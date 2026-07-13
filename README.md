# Competitor Analysis Agent

An automated, AI-assisted competitor research workflow for Antigravity. It navigates competitor products, extracts UX patterns, collects visual evidence, identifies product opportunities, and generates professional research reports.

This repository is designed as an open-source, configurable workflow that anyone can run locally using Model Context Protocol (MCP) servers.

---

## 🚀 Key Features

* **AI-Assisted Automation:** Reduces competitor research time from hours to minutes.
* **Visual Evidence:** Automatically navigates products using Playwright and captures screenshot evidence.
* **UX Pattern Extraction:** Analyzes interaction designs and user flows across competitors instead of in isolation.
* **Opportunity Discovery:** Identifies feature gaps, product strengths/weaknesses, and emerging trends.
* **Stakeholder Reports:** Compiles findings into professional, structured Markdown documents for designers, PMs, and engineering leads.

---

## 📁 Repository Structure

```text
competitor-analysis-agent/
├── README.md               # Project overview and getting started guide
├── LICENSE                 # Open-source MIT license
├── .gitignore              # Git ignore rules
├── workflows/
│   └── competitor-analysis.md  # Main orchestrator workflow for Antigravity
├── skills/                 # Modular, reusable analysis sub-routines (Skills)
│   ├── competitor-discovery/
│   ├── competitor-analysis/
│   ├── ux-pattern-extraction/
│   ├── opportunity-analysis/
│   └── report-generator/
├── templates/              # Reusable output formats
│   ├── report-template.md
│   ├── feature-matrix.md
│   ├── ux-pattern-library.md
│   └── action-plan.md
├── examples/               # Example inputs and generated reports
├── docs/                   # Deep-dive guides (Architecture, Workflow, Setup)
└── config/                 # Installation and configuration files for MCPs
```

---

## 🛠️ Getting Started

### 1. Prerequisites
You need the following installed:
* [Node.js](https://nodejs.org/) (for running MCP servers via `npx`)
* An IDE with Antigravity installed.

### 2. Configure MCP Servers
This workflow utilizes 5 Model Context Protocol (MCP) servers. Follow the instructions in the [Setup Guide](docs/setup.md) and configure your `mcp_config.json` accordingly.

Required MCPs:
* `figma-console` - Bridge to inspect live designs and design system status.
* `playwright` - Automatic browser control for screenshot capture and navigation.
* `fetcher` - Lightweight web scraper.
* `memory` - Persistent knowledge graph storage.
* `filesystem` - Read and write access for local project assets.

Refer to [required-mcps.md](config/required-mcps.md) for detailed configuration schemas.

### 3. Run the Workflow
1. Open the repository workspace in your editor.
2. In the chat interface, run the workflow by pointing to [competitor-analysis.md](workflows/competitor-analysis.md).
3. Follow the guided interactive questions to start analyzing your competitors.

---

## 🤝 Contributing

We welcome contributions! Please see [roadmap.md](docs/roadmap.md) to understand current development priorities or read [architecture.md](docs/architecture.md) to learn how to write custom skills and integrate them with the shared data models.
