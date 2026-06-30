---
name: lint
description: Audit the wiki for quality issues - contradictions, stale content, orphaned pages
---

# /lint - Audit Wiki Quality

You are executing the arm-learn lint workflow. Your task is to traverse all wiki
pages and check for quality issues.

## Before You Begin

1. Read `schema/CLAUDE.md` for conventions and quality standards.
2. Read `schema/config.yaml` for project configuration.
3. Read `schema/prompts/lint.md` for the detailed lint procedure.

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
