# Required MCP Servers Configuration

The Competitor Analysis Workflow requires the following 5 Model Context Protocol (MCP) servers. Place these definitions in your local configuration file (e.g., `mcp_config.json` in your Antigravity IDE configuration directory).

---

## 1. Figma Console Bridge (`figma-console`)
Allows the agent to capture screenshots, inspect design layouts, check design parity, and list variable tokens.

* **Command**: `npx`
* **Args**: `["-y", "figma-console-mcp@latest"]`
* **Env**:
  - `FIGMA_ACCESS_TOKEN`: Your Figma Personal Access Token.
  - `ENABLE_MCP_APPS`: `"true"`

```json
"figma-console": {
  "command": "npx",
  "args": ["-y", "figma-console-mcp@latest"],
  "env": {
    "ENABLE_MCP_APPS": "true",
    "FIGMA_ACCESS_TOKEN": "your_figma_personal_access_token_here"
  }
}
```

---

## 2. Playwright Browser Automation (`playwright`)
Provides programmatic browser interaction, allowing the agent to navigate competitor websites, interact with components, list open tabs, and capture live visual evidence.

* **Command**: `npx`
* **Args**: `["-y", "@playwright/mcp@latest"]`

```json
"playwright": {
  "command": "npx",
  "args": ["-y", "@playwright/mcp@latest"]
}
```

---

## 3. Fetcher Scraper (`fetcher`)
Used for fast, lightweight fetching of competitor landing pages and raw HTML-to-Markdown conversion.

* **Command**: `npx`
* **Args**: `["-y", "fetcher-mcp"]`

```json
"fetcher": {
  "command": "npx",
  "args": ["-y", "fetcher-mcp"]
}
```

---

## 4. Persistent Memory Graph (`memory`)
Provides persistent semantic memory via a knowledge graph. This is useful for retaining cross-competitor patterns and keeping track of observations over long research sessions.

* **Command**: `npx`
* **Args**: `["-y", "@modelcontextprotocol/server-memory"]`

```json
"memory": {
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-memory"]
}
```

---

## 5. Filesystem Access (`filesystem`)
Required to save extracted screenshot assets, draft raw data nodes, and write out completed competitor analysis reports.

* **Command**: `npx`
* **Args**: `["-y", "@modelcontextprotocol/server-filesystem", "/absolute/path/to/your/competitor-analysis-agent"]`

```json
"filesystem": {
  "command": "npx",
  "args": [
    "-y",
    "@modelcontextprotocol/server-filesystem",
    "/Users/sujay/Documents/App Projects/Competitor Analysis Workflow"
  ]
}
```

---

## Full `mcp_config.json` Example

You can merge the following snippet into your IDE config:

```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "ENABLE_MCP_APPS": "true",
        "FIGMA_ACCESS_TOKEN": "YOUR_FIGMA_ACCESS_TOKEN"
      }
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    },
    "fetcher": {
      "command": "npx",
      "args": ["-y", "fetcher-mcp"]
    },
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"]
    },
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/sujay/Documents/App Projects/Competitor Analysis Workflow"
      ]
    }
  }
}
```
