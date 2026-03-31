# Osint-Harvest: Iterative OSINT Scraper

## Overview
This skill spawns a fast, high-volume OSINT harvester. It enumerates accounts and aggressively uses `web_fetch` to scrape bios, posts, and articles, pivoting iteratively on new identifiers to build a raw Data Lake in Markdown format.

## Trigger
When the user asks to harvest OSINT data or runs `/osint-harvest <target>`:
1. Ensure the `reports/` directory exists.
2. Read `/home/lidor_shim/.openclaw/workspace/skills/osint-harvest/AGENT_PROMPT.md` using the `read` tool.
3. Spawn an isolated subagent using the `sessions_spawn` tool.
   - `runtime`: "subagent"
   - `model`: "google/gemini-3-flash-preview" (for speed/cost efficiency)
   - `task`: "Target: <target>\n\n" + [Contents of AGENT_PROMPT.md]
   - `label`: `osint-harvest-<target>`
4. End your turn using `sessions_yield`. The subagent will run its deep-scraping loop and save the raw data to `/home/lidor_shim/.openclaw/workspace/reports/<target>_raw_data.md`.