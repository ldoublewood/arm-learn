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
