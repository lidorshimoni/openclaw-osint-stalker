# OpenClaw OSINT Stalker Plugin 🕵️‍♂️

An automated reconnaissance and Open-Source Intelligence (OSINT) skill for the OpenClaw agent ecosystem. The **Osint-Stalker** subagent takes a single lead (username, email, or phone number) and orchestrates a minimal-overlap stack of FOSS OSINT tools to build a comprehensive dossier without requiring the user to manage individual terminals.

## 🚀 Features
- **Quick vs Deep Scans:** Break down the time complexity of the scan by choosing between a rapid identity resolution sweep or a comprehensive recursive dossier.
- **Academic, Media, & Developer Footprints:** Deep scans pull in Google Scholar publications, news mentions, and Git commit history leaks.
- **Deep Breaches & Pastes:** Integrated with `Mosint`, `WhatBreach`, and `h8mail` to find pastebin dumps and breach datasets.
- **Isolated Execution:** Runs complex OSINT tools via Docker and Python virtual environments.
- **Graceful API Degradation:** Designed to operate seamlessly without API keys.

## 🛠️ Tool Stack
- **Username:** [Maigret](https://github.com/soxoj/maigret) (Recursive Deep) or [Sherlock](https://github.com/sherlock-project/sherlock) (Quick)
- **Email/Breaches/Pastes:** [Mosint](https://github.com/alpkeskin/mosint), [Holehe](https://github.com/megadose/holehe), [WhatBreach](https://github.com/Ekultek/WhatBreach), [h8mail](https://github.com/khast3x/h8mail)
- **Code/Dev:** [Gitrecon](https://github.com/GONZOsint/gitrecon) (GitHub/GitLab commit emails)
- **Academic/Media:** [Senginta](https://github.com/senginta) & OSRFramework (Google Scholar, News)
- **Phone:** [PhoneInfoga](https://github.com/sundowndev/phoneinfoga)

## 📦 Installation
1. Clone this repository into your OpenClaw skills directory:
   ```bash
   cd ~/.openclaw/workspace/skills/
   git clone https://github.com/lidorshimoni/openclaw-osint-stalker osint-stalker
   ```

## 🎮 Usage
Trigger the skill with an optional mode parameter:
```
/osint quick <target>
/osint deep <target>
```

## 📝 Reporting
The subagent yields a Markdown file (`reports/osint_<target>.md`) detailing:
- Executive Summary & Risk Assessment
- Digital Footprint (Accounts & Code)
- Media, Academic & Web Mentions
- Breach & Paste Exposure
- Coverage Gaps & Recommended API Keys
- Next Possible Leads

## 🛡️ Ethics & Constraints
This plugin relies strictly on public APIs, scraped footprints, and OSINT frameworks. It performs passive reconnaissance only. Do not use for unauthorized access or doxxing.