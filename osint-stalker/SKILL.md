# Osint-Stalker: Deep OSINT Subagent

## Overview
This skill spawns a dedicated, highly contextualized OSINT subagent. It supports tiered investigations ("quick" vs "deep") to manage execution time, expanding beyond basic accounts to include academic publications, media mentions, source code footprints, and deep paste/breach data.

## Trigger
When the user requests an OSINT investigation, specify the depth by running `/osint [quick|deep] <target>`. Defaults to `quick` if not specified.
1. Ensure the `reports/` directory exists.
2. Read `/home/lidor_shim/.openclaw/workspace/skills/osint-stalker/AGENT_PROMPT.md` using the `read` tool.
3. Spawn an isolated subagent using the `sessions_spawn` tool.
   - `runtime`: "subagent"
   - `task`: "Target: <target>\nMode: <quick|deep>\n\n" + [Contents of AGENT_PROMPT.md]
   - `label`: `osint-<target>`
4. End your turn using `sessions_yield`. The subagent will run its tiered investigation, save the report to `/home/lidor_shim/.openclaw/workspace/reports/osint_<target>.md`, and return a summary with next leads.