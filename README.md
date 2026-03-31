<p align="center">
  <img src="logo.jpg" alt="Osint-Stalker Logo" width="200" />
</p>

# OpenClaw OSINT Skills (Two-Tier Architecture)

A decoupled, scalable OSINT framework for OpenClaw using dual subagent architectures to separate massive data scraping from intelligent synthesis.

## Architecture

This project has been split into two distinct AgentSkills to maximize efficiency and reasoning capability:

### 1. `osint-harvest` (The Scraping Loop)
- **Model:** Slim, fast models (`google/gemini-3-flash-preview`).
- **Function:** Enumerates targets using tools like `maigret`, then aggressively uses `web_fetch` to scrape the raw contents of profiles, bios, and posts. It scans the raw markdown for new identifiers (emails, links) and pivots iteratively (depth=2).
- **Output:** A massive raw Data Lake stored at `reports/<target>_raw_data.md`.
- **Trigger:** `/osint-harvest <target>`

### 2. `osint-ask` (The Research Engine)
- **Model:** High-reasoning models (`google/gemini-3.1-pro-preview`).
- **Function:** Orchestrates the intelligence cycle. When asked a specific question, it ingests the scraped Data Lake and synthesizes a precise, cited intelligence brief. If the Data Lake doesn't exist, it automatically spawns the `osint-harvest` skill first.
- **Trigger:** `/osint-ask <target> <question>`

## Installation

To test locally in OpenClaw, link both skills:

```bash
openclaw skills install path/to/osint-stalker-repo/osint-harvest
openclaw skills install path/to/osint-stalker-repo/osint-ask
```

## Example Workflow

1. **User:** "What is the last known location of lidorshimoni?"
2. **Orchestrator (`osint-ask`):** Checks if `reports/lidorshimoni_raw_data.md` exists. It doesn't.
3. **Orchestrator:** Spawns `osint-harvest` subagent (Gemini Flash).
4. **Harvester (`osint-harvest`):** Enumerates accounts, scrapes GitHub bios, LinkedIn posts, and personal websites. Dumps raw markdown into the Data Lake.
5. **Orchestrator:** Re-awakens, ingests the massive markdown file, and synthesizes the answer.
6. **Orchestrator:** Replies to the user: "Based on a scraped GitHub bio (`github.com/lidorshimoni`) and a Hackaday project post (`hackaday.io/...`), the last known location is Kiryat Gat, Israel."