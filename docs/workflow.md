# Workflow Execution Guide

This document describes how the Competitor Analysis workflow operates and details the interaction model between the user and the agent.

---

## 🛠️ Execution Process

The workflow runs in a series of guided steps, orchestrating several analysis skills.

```mermaid
sequenceDiagram
    actor User
    participant Agent as Antigravity Agent
    participant Playwright as Playwright MCP
    participant Scraper as Fetcher MCP
    participant Disk as Local Filesystem

    User->>Agent: Run workflows/competitor-analysis.md
    Agent->>User: Launch guided questionnaire
    User->>Agent: Submit goals, domains, & target features
    Agent->>Disk: Write ResearchContext JSON
    
    rect rgb(200, 220, 240)
        note right of Agent: Phase: Competitor Discovery & Scraping
        Agent->>Scraper: Fetch search queries & domain pages
        Scraper-->>Agent: Raw Page text/markdown
        Agent->>Disk: Write enriched CompetitorProfiles
    end

    rect rgb(220, 240, 200)
        note right of Agent: Phase: UX Pattern & Screenshot Capture
        Agent->>Playwright: Launch browser & navigate to targets
        Playwright->>Playwright: Interact, fill forms, scroll
        Playwright->>Disk: Save screenshots under assets/screenshots/
        Agent->>Disk: Write UXPattern models with screenshot paths
    end

    rect rgb(240, 220, 200)
        note right of Agent: Phase: Opportunity & Report Compilation
        Agent->>Agent: Synthesize feature matrix and opportunity models
        Agent->>Disk: Compile report-template.md and save reports/competitor_research_report.md
    end

    Agent-->>User: Output completed report & walk user through findings
```

---

## 🙋 Guided Questionnaire (Initialization)

When you run `workflows/competitor-analysis.md`, the agent prompts you with the following questions:

1. **What is the name of your project or product?** (e.g., *SaaS Subscriptions Tracker*)
2. **What are the primary goals of this research?** (e.g., *Analyze how competitors manage subscription renewals*)
3. **Who is the target audience?** (e.g., *SMB operations managers*)
4. **Who are the competitors to investigate?** (Provide specific URLs, or specify "Discover automatically")
5. **Which user flows or features should we focus on?** (e.g., *Signup flow, renewal alerts, notification settings*)
6. **Should we run Playwright browser scraping live or inspect static Figma designs?** (Options: *Live browser scraping*, *Figma files*, or *Both*)

Once answered, the agent initializes the JSON data schemas and begins executing the active skills sequentially.
