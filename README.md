# OpenClaw OSINT Stalker Plugin 🕵️‍♂️

<p align="center">
  <img src="logo.jpg" alt="Osint-Stalker Logo" width="200" />
</p>

An automated reconnaissance and Open-Source Intelligence (OSINT) skill for the OpenClaw agent ecosystem. The **Osint-Stalker** subagent takes a single lead (username, email, or phone number) and orchestrates a minimal-overlap stack of FOSS OSINT tools to build a comprehensive dossier.

## 🌟 Zero-Config Philosophy
This plugin is designed to work **out of the box**. It strictly prioritizes tools and methods that require **no API keys, no registration, and no complex setup**. Advanced tools that require paid or registered API keys (like deep breach databases) are relegated to an optional tier.

## 🚀 Features
- **Quick vs Deep Scans:** Break down the time complexity. `quick` runs rapid identity sweeps, while `deep` runs recursive profiling and targeted dorking.
- **Keyless Execution:** Relies on Sherlock, Maigret, Holehe, PhoneInfoga, and intelligent Web Search Dorking to bypass API paywalls.
- **Automated Dorking:** For academic publications, news mentions, and pastebin leaks, the subagent uses its native web search capabilities to execute advanced Dorks without requiring finicky scraper setups.
- **Isolated Execution:** Runs complex OSINT tools via Docker and Python virtual environments to keep your host machine clean.

## 🛠️ The Out-of-the-Box Tool Stack
- **Username:** [Maigret](https://github.com/soxoj/maigret) (Deep) or [Sherlock](https://github.com/sherlock-project/sherlock) (Quick) — *Zero keys required.*
- **Email:** [Holehe](https://github.com/megadose/holehe) (Account Mapping) — *Zero keys required.*
- **Code/Dev:** [Gitrecon](https://github.com/GONZOsint/gitrecon) — *Zero keys required (public endpoints).*
- **Phone:** [PhoneInfoga](https://github.com/sundowndev/phoneinfoga) — *Zero keys required for basic scans.*
- **Pastes & Publications:** Executed natively via OpenClaw Web Search Dorking (e.g., `site:pastebin.com`).

*(Optional Advanced Tools like Mosint, WhatBreach, and h8mail are supported if you choose to configure your own API keys, but are safely skipped otherwise).*

## 📦 Installation

To install this skill locally into your OpenClaw workspace:

```bash
cd ~/.openclaw/workspace/skills/
git clone https://github.com/lidorshimoni/openclaw-osint-stalker.git osint-stalker
```

*Note: You can also find and publish OpenClaw plugins on the official community marketplace at [ClawHub.ai](https://clawhub.ai).*

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