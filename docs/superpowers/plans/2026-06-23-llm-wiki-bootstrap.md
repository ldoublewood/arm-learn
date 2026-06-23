# LLM Wiki Bootstrap - Phase 0 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (- [ ]) syntax for tracking.

**Goal:** Bootstrap the arm-learn LLM Wiki: scaffold the three-layer directory structure, write all schema configs and Claude Code skill definitions, then smoke-test with a first ingest.

**Architecture:** This is a Claude-Code-native project. There is no application code - the "runtime" is Claude Code executing skill-defined workflows against Markdown files. All behavior is defined through Markdown skill definitions, YAML configs, and prompt templates.

**Tech Stack:** Claude Code Skills, Markdown + YAML frontmatter, [[wikilinks]], MCP tools (WebFetch, web_search_exa)

---

### Task 1: Scaffold Directory Structure

**Files to create:**
- `raw/_inbox/.gitkeep`, `raw/papers/.gitkeep`, `raw/articles/.gitkeep`, `raw/docs/.gitkeep`
- `wiki/concepts/.gitkeep`, `wiki/papers/.gitkeep`, `wiki/tools/.gitkeep`
- `schema/prompts/.gitkeep`
- `.claude/skills/.gitkeep`

- [ ] **Step 1: Create all directories**

```bash
mkdir -p /t/hub/arm-learn/raw/_inbox
mkdir -p /t/hub/arm-learn/raw/papers
mkdir -p /t/hub/arm-learn/raw/articles
mkdir -p /t/hub/arm-learn/raw/docs
mkdir -p /t/hub/arm-learn/wiki/concepts
mkdir -p /t/hub/arm-learn/wiki/papers
mkdir -p /t/hub/arm-learn/wiki/tools
mkdir -p /t/hub/arm-learn/schema/prompts
mkdir -p /t/hub/arm-learn/.claude/skills
```

- [ ] **Step 2: Add .gitkeep files to preserve empty directories in git**

```bash
touch /t/hub/arm-learn/raw/_inbox/.gitkeep
touch /t/hub/arm-learn/raw/papers/.gitkeep
touch /t/hub/arm-learn/raw/articles/.gitkeep
touch /t/hub/arm-learn/raw/docs/.gitkeep
touch /t/hub/arm-learn/wiki/concepts/.gitkeep
touch /t/hub/arm-learn/wiki/papers/.gitkeep
touch /t/hub/arm-learn/wiki/tools/.gitkeep
touch /t/hub/arm-learn/schema/prompts/.gitkeep
touch /t/hub/arm-learn/.claude/skills/.gitkeep
```

- [ ] **Step 3: Commit scaffold**

```bash
git -C /t/hub/arm-learn add -A
git -C /t/hub/arm-learn commit -m "chore: scaffold LLM wiki directory structure"
```

---

### Task 2: Write schema/CLAUDE.md (Project Constitution)

**Files:**
- Create: `schema/CLAUDE.md`

This is the single most important file in the project. Every LLM operation reads it first to understand conventions, domain scope, page templates, and quality standards.

- [ ] **Step 1: Write schema/CLAUDE.md**

Write the following content to `/t/hub/arm-learn/schema/CLAUDE.md`:

```markdown
# arm-learn - LLM Wiki for Industrial Robotic Arms

## Role

You are the librarian and knowledge compiler for this wiki. Your job is to read raw sources from `raw/` and produce structured, interlinked Markdown knowledge pages in `wiki/`. You maintain the index, enforce conventions, and ensure knowledge compounds rather than fragments.

## Domain Scope

Industrial robotic arms (工业机械臂):

- Kinematics and dynamics (运动学/动力学)
- Trajectory planning (轨迹规划)
- Force control and impedance control (力控/阻抗控制)
- Grasp planning (抓取规划)
- ROS/ROS2 integration
- Visual servoing (视觉伺服)
- Motion planning (运动规划)
- Collision detection (碰撞检测)

## Directory Layout

```
raw/          Immutable sources. READ ONLY. Never modify files here except
              to move them from _inbox/ to their archive directory.
wiki/         LLM-maintained knowledge base. You create and maintain all
              files here.
schema/       Steering configs. Read before every operation.
```

## Page Templates

### Concept Page: wiki/concepts/<slug>.md

---
category: concept
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
related: []
---

# Title (English Term in Parentheses)

## Definition
Clear 2-3 sentence definition.

## Key Principles
- Principle 1
- Principle 2

## Mathematical Foundation
(if applicable - key equations with explanation)

## Related Concepts
- [[concept-a]] - relationship description
- [[concept-b]] - relationship description

## References
- [Source description](raw/papers/filename)

### Paper Note: wiki/papers/<first-author-year-keyword>.md

---
category: paper
title: "Full Paper Title"
authors: [Author 1, Author 2]
year: 2024
venue: "Conference or Journal Name"
source: raw/papers/filename
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Paper Title

## TL;DR
One-paragraph summary of the key contribution.

## Key Contributions
1. Contribution one
2. Contribution two

## Method
Brief description of the approach.

## Results
Key findings and numbers.

## Relevance to Industrial Robotic Arms
How this connects to practical arm control/planning/etc.

## Related Concepts
- [[concept-x]]
- [[concept-y]]

### Tool Page: wiki/tools/<name>.md

---
category: tool
version: ""
ecosystem: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
---

# Tool Name

## Overview
What it does, who makes it, license.

## Key Features
- Feature 1
- Feature 2

## Installation
Basic setup commands.

## Relevance to Industrial Robotic Arms
How this tool is used in the domain.

## Related Concepts
- [[concept-x]]

### Index Page: wiki/index.md

---
category: index
updated: YYYY-MM-DD
---

# arm-learn Knowledge Index

## Concepts
- [[concepts/slug]] - one-line description

## Papers
- [[papers/key]] - one-line summary

## Tools
- [[tools/name]] - one-line description

## Topic Map
(Grouped by sub-domain)
- Kinematics: [[page1]], [[page2]]
- Control: [[page3]], [[page4]]
- ...

## Writing Conventions

1. **Language:** Chinese primary, English terms preserved with (translation) on first use.
   Example: 阻抗控制（impedance control）通过调节...

2. **Links:** Use [[wikilinks]] for internal wiki references. First mention of any
   concept must be linked. Use [描述](raw/...) for citing raw sources.

3. **Page size:** Max 500 lines per concept page. Split into sub-pages if needed.

4. **Naming:**
   - Concept pages: lowercase slug with hyphens, e.g. `impedance-control.md`
   - Paper pages: `firstauthor-year-keyword.md`, e.g. `hogan-1985-impedance-control.md`
   - Tool pages: lowercase tool name, e.g. `ros2-control.md`

5. **Frontmatter:** Every wiki page MUST have YAML frontmatter with at minimum:
   category, created, updated.

6. **Citations:** Always link back to raw source files. Knowledge must be traceable.

## Quality Standards

- Read `wiki/index.md` before every ingest to understand current knowledge state.
- Cross-reference generously: every new concept page should be linked from at least
  one existing page.
- When a new source contradicts an existing claim, flag it with a
  [CONTRADICTION] marker and explain both sides.
- After every ingest, update `wiki/changelog.md` with what was added/changed.
- Never delete content from wiki pages; add updates with "Updated YYYY-MM-DD:" prefix.
```

- [ ] **Step 2: Commit**

```bash
git -C /t/hub/arm-learn add schema/CLAUDE.md
git -C /t/hub/arm-learn commit -m "feat: add project constitution (CLAUDE.md)"
```

---

### Task 3: Write schema/prompts/ingest.md

**Files:**
- Create: `schema/prompts/ingest.md`

Defines the exact behavior specification for the ingest operation. The /ingest skill reads this file and follows its instructions.

- [ ] **Step 1: Write schema/prompts/ingest.md**

```markdown
# Ingest Behavior Specification

## Purpose
Process new raw sources from `raw/_inbox/` and integrate them into the wiki.

## Pre-conditions
- One or more files exist in `raw/_inbox/`
- `schema/CLAUDE.md` has been read for conventions

## Procedure

### 1. Survey
Read ALL files currently in `raw/_inbox/`. For each file, determine:
- Type: paper, article, documentation, or other
- Primary topic(s): which concepts does it cover?
- Quality: is this substantive enough to ingest? (Skip spam, paywalls, empty content)

### 2. Context Loading
Read `wiki/index.md` to understand the current knowledge structure.
Identify which existing pages are related to the new content.

### 3. Page Generation
For each new source, create or update wiki pages following these rules:

**New Concept:** If a concept not yet in the wiki appears:
- Create `wiki/concepts/<slug>.md` using the concept page template
- Add it to `wiki/index.md` under Concepts and the appropriate topic group

**New Paper:** Always create a paper note:
- Create `wiki/papers/<key>.md` using the paper note template
- Extract at minimum: TL;DR, key contributions, method, results, relevance
- Add to `wiki/index.md` under Papers

**New Tool/Framework:** If a tool is discussed:
- Create `wiki/tools/<name>.md` if it does not exist
- Add to `wiki/index.md` under Tools

**Existing Concept Update:** If content adds to an existing concept:
- Append to the concept page with "Updated YYYY-MM-DD: new information"
- Update the `updated` field in frontmatter

### 4. Cross-Referencing
- Ensure every new page links to at least 2 existing pages via [[wikilinks]]
- Add backlinks from existing pages to new pages where appropriate
- First mention of any concept in any page MUST be a [[wikilink]]

### 5. Changelog
Append to `wiki/changelog.md` with format:

```
## YYYY-MM-DD
- **Source:** raw/papers/filename (or raw/articles/filename)
- **New pages:** [[page-a]], [[page-b]]
- **Updated pages:** [[page-c]] (reason)
- **Summary:** one-sentence summary of what was ingested
```

### 6. Archive
Move each processed file from `raw/_inbox/` to the appropriate archive:
- Papers → `raw/papers/`
- Articles → `raw/articles/`
- Documentation → `raw/docs/`

## Post-conditions
- `raw/_inbox/` is empty
- All new knowledge is integrated into wiki pages with [[wikilinks]]
- `wiki/index.md` is updated
- `wiki/changelog.md` has new entries

## Error Handling
- If a source file is unreadable or empty: move to `raw/_inbox/` with a suffix `.skipped` and note in changelog
- If a topic is outside the domain scope: still ingest but mark with tag `peripheral`
- If contradictory claims found: flag with `[CONTRADICTION: ...]` marker, do not silently resolve
```

- [ ] **Step 2: Commit**

```bash
git -C /t/hub/arm-learn add schema/prompts/ingest.md
git -C /t/hub/arm-learn commit -m "feat: add ingest behavior specification"
```

---

### Task 4: Write schema/prompts/lint.md

**Files:**
- Create: `schema/prompts/lint.md`

- [ ] **Step 1: Write schema/prompts/lint.md**

```markdown
# Lint Behavior Specification

## Purpose
Periodically audit the wiki for quality issues: contradictions, stale content, orphaned pages, broken links, index omissions.

## Procedure

### 1. Full Traversal
Read every .md file in `wiki/`. Build a mental map of:
- All pages and their `updated` dates
- All [[wikilinks]] (source → target mapping)
- All categories and tags

### 2. Checks

**Contradictions:**
- Scan for [CONTRADICTION] markers
- Review whether they have been resolved
- If unresolved for > 90 days, flag in report

**Stale Content:**
- Pages with `updated` date > 180 days ago
- Mark with "Last updated: YYYY-MM-DD - may need review" banner

**Orphaned Pages:**
- Pages with zero incoming [[wikilinks]] (no other page links to them)
- List them in the report
- If truly orphaned and peripheral, consider removing from index

**Broken Links:**
- [[wikilinks]] that point to non-existent wiki pages
- List them; suggest whether to create the target page or remove the link

**Index Omissions:**
- Pages that exist but are not listed in `wiki/index.md`
- Add them to index

**Missing Backlinks:**
- When page A links to page B, page B should ideally link back or at least mention A
- Flag unidirectional links for review

### 3. Auto-Fixes
These can be applied without human review:
- Add missing pages to `wiki/index.md`
- Update `updated` dates in frontmatter
- Fix obvious typos in [[wikilinks]] (e.g., misspelled page names)

### 4. Report
Output a lint report with sections:
- **Issues Fixed:** (auto-fixes applied)
- **Warnings:** (stale pages, orphaned pages, missing backlinks)
- **Action Required:** (contradictions needing resolution, broken links needing decisions)

Update `wiki/orphaned.md` with current orphaned page list.

## Post-conditions
- All auto-fixable issues resolved
- `wiki/orphaned.md` up to date
- Lint report presented to user
```

- [ ] **Step 2: Commit**

```bash
git -C /t/hub/arm-learn add schema/prompts/lint.md
git -C /t/hub/arm-learn commit -m "feat: add lint behavior specification"
```

---

### Task 5: Write schema/sources.yaml

**Files:**
- Create: `schema/sources.yaml`

Starter curated source list for industrial robotic arms.

- [ ] **Step 1: Write schema/sources.yaml**

```yaml
# Curated sources for industrial robotic arms knowledge
# Phase 2: auto-discovery will poll these for new content

sources:
  # Academic papers
  - name: arXiv - Robotics (cs.RO)
    url: https://arxiv.org/list/cs.RO/recent
    type: rss
    category: papers
    language: english

  - name: arXiv - Systems and Control (cs.SY)
    url: https://arxiv.org/list/cs.SY/recent
    type: rss
    category: papers
    language: english

  - name: IEEE RAS publications
    url: https://www.ieee-ras.org/publications
    type: web
    category: papers
    language: english

  # Documentation
  - name: ROS 2 Documentation (Rolling)
    url: https://docs.ros.org/en/rolling/
    type: doc
    category: tools
    language: english

  - name: MoveIt 2 Documentation
    url: https://moveit.picknik.ai/main/
    type: doc
    category: tools
    language: english

  - name: Gazebo Simulation Docs
    url: https://gazebosim.org/docs/latest
    type: doc
    category: tools
    language: english

  - name: ros2_control Documentation
    url: https://control.ros.org/master/
    type: doc
    category: tools
    language: english

  # Community
  - name: ROS Discourse
    url: https://discourse.ros.org/
    type: forum
    category: articles
    language: english

  # Chinese sources
  - name: 知乎 - 机器人话题
    url: https://www.zhihu.com/topic/19563833
    type: social
    category: articles
    language: chinese

  - name: 知乎 - ROS话题
    url: https://www.zhihu.com/topic/20022224
    type: social
    category: articles
    language: chinese
```

- [ ] **Step 2: Commit**

```bash
git -C /t/hub/arm-learn add schema/sources.yaml
git -C /t/hub/arm-learn commit -m "feat: add curated source list for robotic arms"
```

---

### Task 6: Write Claude Code Skill - /ingest

**Files:**
- Create: `.claude/skills/ingest.md`

This is the Claude Code custom skill that orchestrates the full ingest workflow.

- [ ] **Step 1: Write .claude/skills/ingest.md**

```markdown
---
name: ingest
description: Process new raw sources from raw/_inbox/ and integrate them into the wiki
---

# /ingest - Ingest New Knowledge

You are executing the arm-learn ingest workflow. Your task is to read new sources
from `raw/_inbox/` and integrate them into the LLM-maintained wiki.

## Before You Begin

1. Read `schema/CLAUDE.md` for the project constitution, domain scope, page templates,
   and writing conventions.
2. Read `schema/prompts/ingest.md` for the detailed ingest procedure.
3. List files in `raw/_inbox/`. If empty, tell the user there is nothing to ingest.

## Execution

Follow the procedure defined in `schema/prompts/ingest.md` exactly. The key steps:

1. **Survey** - Read all files in `raw/_inbox/`, determine type/topic/quality
2. **Context** - Read `wiki/index.md` to understand current knowledge structure
3. **Generate** - Create or update wiki pages following the templates in CLAUDE.md
4. **Cross-reference** - Add [[wikilinks]] generously; every new page links to 2+ existing pages
5. **Changelog** - Append to `wiki/changelog.md`
6. **Archive** - Move processed files from `raw/_inbox/` to their archive directory

## Important Rules

- NEVER modify files in `raw/` except to move them from `_inbox/` to their archive
- ALWAYS create frontmatter on every wiki page
- ALWAYS update `wiki/index.md` when adding new pages
- NEVER delete content from wiki pages; append updates with date prefix
- If contradictions found, flag with `[CONTRADICTION: ...]` - do not silently resolve
```

- [ ] **Step 2: Commit**

```bash
git -C /t/hub/arm-learn add .claude/skills/ingest.md
git -C /t/hub/arm-learn commit -m "feat: add /ingest Claude Code skill"
```

---

### Task 7: Write Claude Code Skill - /lint

**Files:**
- Create: `.claude/skills/lint.md`

- [ ] **Step 1: Write .claude/skills/lint.md**

```markdown
---
name: lint
description: Audit the wiki for quality issues - contradictions, stale content, orphaned pages
---

# /lint - Audit Wiki Quality

You are executing the arm-learn lint workflow. Your task is to traverse all wiki
pages and check for quality issues.

## Before You Begin

1. Read `schema/CLAUDE.md` for conventions and quality standards.
2. Read `schema/prompts/lint.md` for the detailed lint procedure.

## Execution

Follow the procedure defined in `schema/prompts/lint.md` exactly:

1. **Traverse** - Read every .md file in `wiki/`
2. **Check** - Look for: contradictions, stale pages (>180 days), orphaned pages,
   broken [[wikilinks]], index omissions, missing backlinks
3. **Auto-fix** - Fix what you can: add missing pages to index, fix obvious typos
4. **Report** - Output a structured lint report with: Issues Fixed, Warnings, Action Required
5. **Update** - Refresh `wiki/orphaned.md`

## Output Format

Present findings as:

### Lint Report - YYYY-MM-DD

**Issues Fixed (N):**
- item 1
- item 2

**Warnings (N):**
- item 1
- item 2

**Action Required (N):**
- item 1 (explanation)
- item 2 (explanation)
```

- [ ] **Step 2: Commit**

```bash
git -C /t/hub/arm-learn add .claude/skills/lint.md
git -C /t/hub/arm-learn commit -m "feat: add /lint Claude Code skill"
```

---

### Task 8: Write Claude Code Skill - /search

**Files:**
- Create: `.claude/skills/search.md`

- [ ] **Step 1: Write .claude/skills/search.md**

```markdown
---
name: search
description: Search the web for knowledge on a topic, save results to raw/_inbox/, then trigger ingest
---

# /search - Web Search and Ingest

You are executing the arm-learn search workflow. This supplements the wiki
with web search results on a given topic.

## Before You Begin

Read `schema/CLAUDE.md` for domain scope context.

## Execution

1. **Search** - Use the web_search_exa MCP tool with the user's keyword query.
   Append relevant domain terms to focus results (e.g., "robotic arm", "manipulator",
   "industrial robot", "机械臂").

2. **Filter** - From the search results, select 3-5 most relevant items that:
   - Are within the industrial robotic arms domain scope
   - Are substantive (not just link aggregations or spam)
   - Provide new information likely not already in the wiki

3. **Capture** - For each selected result, use WebFetch to retrieve full content.
   Save each to `raw/_inbox/<YYYY-MM-DD-source-title>.md` with format:

   ```markdown
   # Source Title
   **URL:** https://...
   **Date captured:** YYYY-MM-DD
   **Source type:** web article / paper / documentation

   ---
   (full content in markdown)
   ```

4. **Ingest** - After all results are saved to `raw/_inbox/`, follow the ingest
   procedure defined in `schema/prompts/ingest.md` to integrate them into the wiki.

## Quality Gate

- Skip paywalled content (note in changelog)
- Skip content clearly outside domain scope
- If search returns nothing useful, report honestly and do not force ingestion
```

- [ ] **Step 2: Commit**

```bash
git -C /t/hub/arm-learn add .claude/skills/search.md
git -C /t/hub/arm-learn commit -m "feat: add /search Claude Code skill"
```

---

### Task 9: Smoke Test - First Ingest

**Files:**
- Create: `raw/_inbox/test-article.md` (sample source)
- Will create: `wiki/index.md`, `wiki/concepts/*.md`, `wiki/changelog.md`

This task validates the entire pipeline end-to-end by ingesting a real article.

- [ ] **Step 1: Drop a sample source into _inbox**

Use WebFetch to capture a real, high-quality article about impedance control and save it:

```bash
# The ingest skill will use WebFetch, but we pre-populate _inbox for the test
cat > /t/hub/arm-learn/raw/_inbox/2026-06-23-impedance-control-intro.md << 'EOF'
# An Introduction to Impedance Control for Robotic Manipulators

**Source URL:** https://example.com/impedance-control-intro (sample)

## What is Impedance Control?

Impedance control is a approach to dynamic control of robotic manipulators
pioneered by Neville Hogan in 1985. Unlike traditional position control which
commands exact joint angles, impedance control regulates the dynamic
relationship between the manipulator's motion and the forces it exerts on the
environment.

The core idea: instead of controlling position OR force exclusively, impedance
control allows the robot to behave like a mass-spring-damper system. When the
environment pushes on the robot, the robot yields with a specified stiffness
and damping, rather than fighting to maintain an exact position.

## The Mathematical Model

The target impedance is typically expressed as:

    M(x_ddot - x_ddot_d) + B(x_dot - x_dot_d) + K(x - x_d) = F_ext

Where:
- M is the desired inertia matrix
- B is the desired damping matrix
- K is the desired stiffness matrix
- x is actual position, x_d is desired position
- F_ext is the external force

## Key Applications

1. **Assembly tasks** - The robot can comply when inserting parts, preventing
   jamming and damage.

2. **Polishing and grinding** - Maintaining consistent force while following
   curved surfaces.

3. **Human-robot interaction** - Making the robot safe and compliant when
   humans are nearby.

4. **Unknown environments** - The robot can adapt to uncertain contact
   conditions.

## Relationship to Admittance Control

Impedance control assumes the robot is a mechanical impedance (accepts force
input, produces motion output). Admittance control is the dual: the robot is
a mechanical admittance (accepts motion input, produces force output).

Impedance control is preferred for lightweight, backdrivable robots.
Admittance control is preferred for heavy, non-backdrivable industrial arms.

## ROS2 Implementation

The `ros2_control` framework provides impedance control implementations
through its controller interface. Key packages include:
- `joint_trajectory_controller`
- `force_torque_sensor_broadcaster`
- `impedance_control` (community package)
EOF
```

- [ ] **Step 2: Run the /ingest skill**

Execute `/ingest` in Claude Code. The LLM should:
1. Read `raw/_inbox/` → find the sample article
2. Read `schema/CLAUDE.md` → understand conventions
3. Read `wiki/index.md` → first time: file does not exist, so create it
4. Generate wiki pages:
   - `wiki/index.md` (initial index)
   - `wiki/concepts/impedance-control.md` (concept page)
   - `wiki/concepts/admittance-control.md` (or merged into impedance page)
   - `wiki/tools/ros2-control.md` (tool page)
   - `wiki/changelog.md` (first entry)
5. Archive: `mv raw/_inbox/test-article.md raw/articles/`

- [ ] **Step 3: Verify outputs**

Check that the following files exist and look correct:

```bash
ls -la /t/hub/arm-learn/wiki/index.md
ls -la /t/hub/arm-learn/wiki/concepts/
ls -la /t/hub/arm-learn/wiki/changelog.md
ls -la /t/hub/arm-learn/raw/articles/2026-06-23-impedance-control-intro.md
# _inbox should be empty
ls -la /t/hub/arm-learn/raw/_inbox/
```

Verify at minimum:
- `wiki/index.md` has frontmatter with category: index
- Concept pages have proper YAML frontmatter with category/tags/related
- `wiki/changelog.md` records the ingest
- Source file was moved from `_inbox/` to `raw/articles/`
- All internal links use [[wikilinks]] syntax

- [ ] **Step 4: Commit the first wiki**

```bash
git -C /t/hub/arm-learn add wiki/ raw/
git -C /t/hub/arm-learn commit -m "feat: first ingest - impedance control"

Co-Authored-By: Claude <noreply@anthropic.com>"
```

