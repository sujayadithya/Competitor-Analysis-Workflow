---
name: competitor-analysis
description: Perform deep qualitative and quantitative audit on discovered competitors, extracting features, navigation, IA, screenshots, and strengths/weaknesses.
---

# Competitor Analysis Skill

This skill scrapes and audits competitor web applications to collect feature inventories, navigation layouts, information architecture, screenshots, strengths, and weaknesses.

## Input Data
- `competitor_profiles.json` (from the competitor-discovery skill)
- `research_scope.json` (from the research-scope skill)

## Collected Fields & Schema Extensions
This skill enriches each profile in `competitor_profiles.json` with the following structured blocks:

* **`screenshots`**: Links to captured landing and pricing screenshots.
  - `landingPage`: `"string (relative path)"`
  - `pricingPage`: `"string (relative path)"`
* **`navigationAnalysis`**: Qualitative summary of the primary navigation layout (e.g. "Sticky top bar with side drawer for settings").
* **`informationArchitecture`**: Array of paths parsed from navigation menus (e.g. `["/pricing", "/features/billing", "/docs/api"]`).
* **`featureInventory`**: Array of objects auditing features from the `research_scope.json` categories:
  - `featureName`: Category audited (e.g., `"Onboarding"`).
  - `status`: `"Supported"` | `"Partial"` | `"Unsupported"`.
  - `notes`: Description of the competitor's implementation.
* **`observations`**: Array of research notes and UX patterns identified during inspection.
* **`positioningStatement`**: Core marketing tagline or value proposition.
* **`strengths`**: Array of product advantages.
* **`weaknesses`**: Array of product disadvantages.

---

## Execution Steps

For each competitor in `competitor_profiles.json`:

### 1. Crawl Homepage & Key Pages
1. Use the `fetcher` MCP to scrape the competitor's homepage and pricing page HTML content, converting them into readable Markdown.
2. Read `research_scope.json` to identify other pages that need to be audited (e.g. if "AI" is selected, find the "/ai" or "/features/ai" page and crawl it).

### 2. Capture Screenshots (Visual Evidence)
1. Initialize the `playwright` MCP browser session.
2. Navigate to the competitor homepage and capture a full-page screenshot. Save to `assets/screenshots/competitor-{{name}}-landing.png`.
3. Navigate to the pricing page and capture a screenshot. Save to `assets/screenshots/competitor-{{name}}-pricing.png`.

### 3. Analyze Navigation & Information Architecture (IA)
1. Parse navigation elements (links, dropdown submenus) in the fetched HTML or browser page.
2. Extract the Information Architecture (IA) mapping of major routing paths.
3. Summarize the navigation pattern (e.g., double top navigation bar, persistent left sidebar).

### 4. Audit Feature Inventory
1. For each category selected in `research_scope.json` (e.g., Onboarding, Tables, AI), search the scraped competitor data.
2. Verify support status (Supported/Partial/Unsupported) and add specific notes detailing how the feature operates.

### 5. Identify Strengths, Weaknesses, and Positioning
1. Analyze homepage copywriting to extract their positioning statement.
2. Compare features and user flow complexities to write down at least 2 strengths and 2 weaknesses.
3. Save miscellaneous notes in the `observations` field.

### 6. Overwrite Competitor Profiles
- Update each competitor object with the newly gathered fields and overwrite `competitor_profiles.json` in the workspace root.

---

## Output Data
- Overwrites the enriched `competitor_profiles.json` file in the workspace root.
