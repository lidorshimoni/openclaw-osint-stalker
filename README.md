<p align="center">
  <img src="logo.jpg" alt="Osint-Stalker Logo" width="200" />
</p>

# OpenClaw OSINT Skill (Unified Architecture)

A decoupled, scalable OSINT framework for OpenClaw using an intelligent Director-Worker architecture to separate massive data scraping from high-level reasoning.

## Architecture: One Command, Two Agents

This skill abstracts complex multi-model pipelines into a single command. 

### `osint` (The Unified Entry Point)
- **Trigger:** `/osint <target> [optional question]`
- **The Flow:**
  1. **The Director (Pro Model):** OpenClaw spawns a high-reasoning "OSINT Director" agent. It ingests your question and checks if a raw data lake exists for the target.
  2. **The Worker (Flash Model):** If data is missing, the Director automatically spawns its own "Harvester" subagent using a fast, low-cost model (`gemini-3-flash-preview`). The Harvester runs deep web scrapes, pivoting through emails and aliases, dumping everything into a massive Markdown file (`reports/<target>_raw_data.md`).
  3. **The Synthesis:** The Director wakes back up, reads the massive raw data lake, cross-references timelines and bios, and synthesizes a precise, cited intelligence brief for the user.

## Installation

Link the skill into your OpenClaw workspace:

```bash
openclaw skills install path/to/osint-stalker-repo/osint
```

## Example Workflow

1. **User:** "What is the last known location of lidorshimoni?"
2. **Orchestrator (`osint-director`):** Checks if `reports/lidorshimoni_raw_data.md` exists. It doesn't.
3. **Orchestrator:** Spawns `osint-harvester` subagent (Gemini Flash).
4. **Harvester:** Enumerates accounts, scrapes GitHub bios, LinkedIn posts, and personal websites. Dumps raw markdown into the Data Lake.
5. **Orchestrator:** Re-awakens, ingests the massive markdown file, and synthesizes the answer.
6. **Orchestrator:** Replies to the user: "Based on a scraped GitHub bio (`github.com/lidorshimoni`) and a Hackaday project post (`hackaday.io/...`), the last known location is Kiryat Gat, Israel."