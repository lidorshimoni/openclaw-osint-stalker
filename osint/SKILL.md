# Osint: Deep OSINT Research Framework

## Overview
This skill acts as the entry point for deep, iterative OSINT research. It triggers an autonomous "Director" agent (Pro model) which orchestrates the investigation. If raw data needs to be gathered, the Director will automatically spawn a "Harvester" subagent (Flash model) to aggressively scrape the web before synthesizing the final intelligence report.

## Trigger
When the user asks to investigate a target or runs `/osint <target> [optional question]`:
1. Ensure the `reports/` directory exists or let the subagent create it.
2. Read the following files using the `read` tool:
   - `/home/lidor_shim/.openclaw/workspace/skills/osint/DIRECTOR_PROMPT.md`
   - `/home/lidor_shim/.openclaw/workspace/skills/osint/HARVESTER_PROMPT.md`
3. Spawn an isolated subagent using the `sessions_spawn` tool.
   - `runtime`: "subagent"
   - `model`: "google/gemini-3.1-pro-preview" (This is the Orchestrator/Director)
   - `label`: `osint-<target>`
   - `task`: Provide the target, the user's question, and both prompts. Tell the Director to follow the DIRECTOR_PROMPT, and provide it the HARVESTER_PROMPT so it can pass it to the Harvester if needed.
   
Example `task` string:
```
Target: <target>
User Question: <question>

You are the OSINT Director. Follow these instructions:
=== DIRECTOR PROMPT ===
[Insert contents of DIRECTOR_PROMPT.md]

If you need to spawn a Harvester, provide it with these instructions:
=== HARVESTER PROMPT ===
[Insert contents of HARVESTER_PROMPT.md]
```
4. End your turn using `sessions_yield`. The Director will orchestrate the harvest and analysis, returning the final report to the user.