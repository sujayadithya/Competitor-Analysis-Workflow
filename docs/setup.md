# Setup & Installation Guide

This document describes how to configure your environment to run the Competitor Analysis workflow.

---

## 💻 System Configuration

To run this workflow, you need an IDE integrated with Antigravity and access to the necessary MCP servers.

### Step 1: Clone the Repository
Clone this repository to your local development environment:
```bash
git clone https://github.com/your-username/competitor-analysis-workflow.git
cd competitor-analysis-workflow
```

### Step 2: Configure MCP Servers in Antigravity
Open your IDE's `mcp_config.json` configuration file. You can locate your IDE's config path by running `list_permissions` or reviewing your environment documentation.

Add the required servers described in [required-mcps.md](../config/required-mcps.md). Ensure that:
- The path to `@modelcontextprotocol/server-filesystem` points to the absolute path of this cloned repository.
- Your `FIGMA_ACCESS_TOKEN` is correctly set in the environment variables for the `figma-console` MCP.

### Step 3: Run the Workflow
1. Start a conversation with the Antigravity agent in the workspace.
2. Type a command prompting the agent to start the research, e.g.:
   > "Run workflows/competitor-analysis.md"
3. The agent will read the workflow orchestrator, initiate the guided questionnaire, and perform the sequential analysis steps.
