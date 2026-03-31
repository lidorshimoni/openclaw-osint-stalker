# Osint-Stalker: Deep OSINT Subagent

## Overview
This skill acts as a router to spawn a dedicated, highly contextualized OSINT subagent. It researches targets using tools like Maigret, Holehe, h8mail, and PhoneInfoga, working with or without API keys, and saves a comprehensive dossier to the `reports/` directory.

## Trigger
When the user requests an OSINT investigation, footprinting, or runs `/osint <target>`:
1. Ensure the `reports/` directory exists or let the subagent create it.
2. Read `/home/lidor_shim/.openclaw/workspace/skills/osint-stalker/AGENT_PROMPT.md` using the `read` tool.
3. Spawn an isolated subagent using the `sessions_spawn` tool.
   - `runtime`: "subagent"
   - `task`: "Target: <target>\n\n" + [Contents of AGENT_PROMPT.md]
   - `label`: `osint-<target>`
4. End your turn using `sessions_yield`. The subagent will run its investigation, save the report to `/home/lidor_shim/.openclaw/workspace/reports/osint_<target>.md`, and return a summary with next leads.