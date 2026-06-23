# arm-learn — LLM Wiki for Industrial Robotic Arms

Date: 2026-06-23 | Status: Approved

## Overview

基于 Andrej Karpathy 的 LLM Wiki 理念，构建一个聚焦工业机械臂的知识库。采用三层架构（`raw/` → `wiki/` → `schema/`），以 Claude Code 原生方式驱动采集、编译和查询。

### Core Vision

> "Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase."

文件即知识库，Claude Code Skills 是操作入口。不引入不必要的框架和数据库——Markdown 文件 + `[[wikilinks]]` 就是全部存储。

---

## 1. Directory Structure

```
/t/hub/arm-learn/
├── raw/                    # Immutable sources (read-only)
│   ├── _inbox/             # Staging area for new captures
│   ├── papers/             # Papers (arXiv, IEEE, etc.)
│   ├── articles/           # Web articles, blog posts
│   └── docs/               # Official documentation captures
│
├── wiki/                   # LLM-maintained knowledge base
│   ├── index.md            # Global index + navigation
│   ├── concepts/           # Concept pages ([[wikilinks]] interlinked)
│   ├── papers/             # Paper notes (one per paper)
│   ├── tools/              # Tools & frameworks (ROS2, MoveIt, Gazebo...)
│   ├── changelog.md        # Ingest change log
│   └── orphaned.md         # Orphaned page tracker (lint output)
│
├── schema/                 # Steering configuration
│   ├── CLAUDE.md           # Project constitution (LLM behavior rules)
│   ├── prompts/            # Ingest/lint prompt templates
│   │   ├── ingest.md       # Ingest behavior specification
│   │   └── lint.md         # Lint behavior specification
│   └── sources.yaml        # Curated source list
│
└── .claude/skills/         # Claude Code skill definitions
    ├── ingest.md           # /ingest skill
    ├── lint.md             # /lint skill
    └── search.md           # /search skill
```

---

## 2. Domain Scope

聚焦**工业机械臂**，包括以下子方向：

- 运动学 / 动力学 (kinematics / dynamics)
- 轨迹规划 (trajectory planning)
- 力控 / 阻抗控制 (force / impedance control)
- 抓取规划 (grasp planning)
- ROS / ROS2 集成
- 视觉伺服 (visual servoing)
- 运动规划 (motion planning)
- 碰撞检测 (collision detection)

### Language Policy

- 采集：中英双语
- Wiki 写作：中文为主，英文术语保留原名 + 中文翻译
- 首次出现的术语格式：`阻抗控制（impedance control）`

---

## 3. Core Workflows

### 3.1 Ingest (`/ingest`)

Trigger: User provides URL or keyword.

```
User input (URL or keyword)
        ↓
[Capture] WebFetch / web_search_exa → raw/_inbox/<date-source-title>.md
        ↓
[Compile] LLM reads _inbox files + wiki/index.md
        ↓
[Write]  LLM creates/updates wiki pages:
         - New entity/concept pages
         - Updated index.md
         - [[cross-references]] in related pages
         - Changelog entry
        ↓
[Archive] mv raw/_inbox/<file> → raw/papers/ or raw/articles/
```

**Key contract:** Each ingest only processes files in `raw/_inbox/`. After processing, files are archived. This prevents duplicate processing and enables traceability.

### 3.2 Lint (`/lint`)

```
LLM traverses all wiki/ pages
        ↓
Checks: contradictions? stale info? orphaned pages?
        missing backlinks? index.md omissions?
        ↓
Output report + auto-fix resolvable issues
        ↓
Unresolvable issues → wiki/orphaned.md + marked "TODO"
```

### 3.3 Query

User asks questions directly in conversation. LLM reads `wiki/index.md` → follows `[[wikilinks]]` → answers with wiki page citations. No additional tooling required.

### 3.4 Search (`/search`)

Supplement knowledge base with web search:

```
Keyword → WebSearch → results → raw/_inbox/ → auto-trigger ingest
```

---

## 4. Schema Layer

### 4.1 `schema/CLAUDE.md`

Project constitution read by LLM before every operation. Defines:
- Domain scope and boundaries
- Page templates (concept, paper, tool)
- Writing conventions (language, formatting, link rules)
- Quality standards

### 4.2 Page Templates

**Concept page** (`wiki/concepts/<name>.md`):
```yaml
---
category: concept
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
related: [[page1]], [[page2]]
---
```

**Paper note** (`wiki/papers/<key>.md`):
```yaml
---
category: paper
title: "..."
authors: [...]
year: 2024
source: raw/papers/<filename>
---
```

**Tool page** (`wiki/tools/<name>.md`):
```yaml
---
category: tool
version: "..."
ecosystem: [ROS2, ...]
---
```

### 4.3 `schema/sources.yaml`

Curated source list for automated discovery (Phase 2):
```yaml
sources:
  - name: arXiv Robotics
    url: https://arxiv.org/list/cs.RO/recent
    type: rss
    category: papers
  - name: ROS 2 Documentation
    url: https://docs.ros.org/en/rolling/
    type: doc
    category: tools
```

---

## 5. Writing Conventions

- Language: Chinese primary, English terms preserved with translation
- Max 500 lines per concept page
- `[[wikilinks]]` must be created on first mention
- Citation format: `[来源](raw/papers/xxx)`
- All pages use Obsidian-compatible `[[wikilinks]]` (not `[text](path.md)`)

---

## 6. Automation Model

**Phase 0 (current):** Manual trigger. User provides URL/keyword → Claude Code executes ingest.

**Phase 1:** Refine schema templates. Accumulate 10-20 concept pages. Validate structure.

**Phase 2:** Introduce `sources.yaml` auto-discovery. Scheduled check of source list; new content auto-enters `_inbox`.

**Phase 3:** MkDocs + Material theme → static site generation → deploy to GitHub Pages.

**Phase 4:** Introduce hybrid search (BM25 + vector) via `qmd` when wiki exceeds 200+ pages.

---

## 7. Tech Choices

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Capture | WebFetch, web_search_exa (MCP) | Already available in Claude Code |
| LLM | Claude (via Claude Code) | Native, no API integration needed |
| Storage | Markdown files + [[wikilinks]] | Karpathy's model, Obsidian-compatible |
| Browsing (local) | Obsidian / VS Code | Graph view, backlinks, search |
| Browsing (web) | MkDocs + Material (Phase 3) | Zero-config static site from Markdown |
| Search (large scale) | qmd (Phase 4) | BM25 + vector hybrid, MCP interface |

---

## 8. Key Design Decisions

1. **Claude Code native over custom app** — Fastest path to working system. The LLM is already here.
2. **Manual trigger over full automation** — Quality gate. Every ingest is reviewed via changelog.
3. **Files over database** — Git-trackable, Obsidian-browsable, no lock-in.
4. **`raw/_inbox/` as staging** — Clear boundary between captured and processed. Enables idempotent ingest.
5. **Schema as code** — `CLAUDE.md` + prompt templates are version-controlled and iterable.

---

## 9. Future Considerations

- **Governance at scale:** When wiki exceeds 200 pages, consider split into sub-indexes
- **Bilingual alignment:** Ensure Chinese/English terminology mapping stays consistent
- **Contradiction resolution:** Define escalation path when LLM detects conflicting claims
- **Collaboration:** Currently single-user; multi-user would require merge conflict handling on wiki files
