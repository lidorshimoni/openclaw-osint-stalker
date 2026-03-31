# OpenClaw OSINT Stalker Plugin 🕵️‍♂️

An automated reconnaissance and Open-Source Intelligence (OSINT) skill for the OpenClaw agent ecosystem. The **Osint-Stalker** subagent takes a single lead (username, email, or phone number) and orchestrates a minimal-overlap stack of FOSS OSINT tools to build a comprehensive dossier without requiring the user to manage individual terminals.

## 🚀 Features
- **Isolated Execution:** Runs complex OSINT tools via Docker and Python virtual environments directly within an isolated subagent session.
- **Tool Chaining & Pivoting:** The subagent doesn't just stop at the first tool. If a username scan reveals an email, it automatically pivots to run email footprinting on that new lead.
- **Graceful API Degradation:** Designed to operate seamlessly without API keys. If rate limits are hit (e.g., `h8mail` with HIBP), it logs the gap and continues.
- **Persistent Reports:** Automatically generates and saves a clean, structured Markdown dossier to your `reports/` folder.

## 🛠️ Tool Stack
- **Username:** [Maigret](https://github.com/soxoj/maigret) (Primary) or [Sherlock](https://github.com/sherlock-project/sherlock) (Fallback)
- **Email:** [Holehe](https://github.com/megadose/holehe) (Account Mapping) and [h8mail](https://github.com/khast3x/h8mail) (Breach checking)
- **Phone:** [PhoneInfoga](https://github.com/sundowndev/phoneinfoga) (Carrier & footprinting)
- **Infrastructure:** [theHarvester](https://github.com/laramies/theHarvester)

## 📦 Installation
1. Clone this repository into your OpenClaw skills directory:
   ```bash
   cd ~/.openclaw/workspace/skills/
   git clone https://github.com/lidorshimoni/openclaw-osint-stalker osint-stalker
   ```
2. Ensure you have Docker installed and running on the host machine, as the subagent relies heavily on containerized execution for OPSEC.

## 🎮 Usage
Trigger the skill in your OpenClaw session by typing:
```
/osint <username|email|phone>
```
Or simply ask:
```
"Investigate lidorshimoni"
```

## 📝 Reporting
The subagent will yield a comprehensive markdown file (`reports/osint_<target>.md`) detailing:
- Executive Summary & Risk Assessment
- Linked Identities & Pivots
- Digital Footprint
- Breach Exposure
- Coverage Gaps & Recommended API Keys
- Next Possible Leads

## 🛡️ Ethics & Constraints
This plugin relies strictly on public APIs, scraped footprints, and OSINT frameworks. It performs passive reconnaissance only. Do not use for unauthorized access or doxxing.