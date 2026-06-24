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
