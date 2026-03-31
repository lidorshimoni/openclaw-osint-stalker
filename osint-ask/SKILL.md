# Osint-Ask: OSINT Research Analyst

## Overview
This skill acts as an orchestrator and analyst. It answers specific research questions using pre-gathered OSINT data. If the data does not exist, it triggers the harvest phase first.

## Trigger
When the user asks a specific question about a target (e.g., "What is the last known location of X?" or `/osint-ask <target> <question>`):
1. Check if `/home/lidor_shim/.openclaw/workspace/reports/<target>_raw_data.md` exists using `exec ls`.
2. **If it DOES NOT exist:** Inform the user that you must harvest the data first. Spawn the `osint-harvest` subagent (following its SKILL.md), and wait for it to complete. Once complete, proceed to step 3.
3. **If it DOES exist:** Read `/home/lidor_shim/.openclaw/workspace/skills/osint-ask/AGENT_PROMPT.md` using the `read` tool.
4. Spawn a high-reasoning subagent using `sessions_spawn`.
   - `runtime`: "subagent"
   - `model`: "google/gemini-3.1-pro-preview" (for complex synthesis)
   - `task`: "Target: <target>\nQuestion: <question>\nData Path: /home/lidor_shim/.openclaw/workspace/reports/<target>_raw_data.md\n\n" + [Contents of AGENT_PROMPT.md]
   - `label`: `osint-ask-<target>`
5. End your turn using `sessions_yield`. The subagent will read the data, synthesize the answer, and report back.