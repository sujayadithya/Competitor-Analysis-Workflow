---
name: competitor-discovery
description: Discover and list relevant market competitors using Playwright and Fetcher, supporting manual overrides and structured categorization.
---

# Competitor Discovery Skill

This skill identifies and categorizes key market competitors by leveraging automated search scraping (using Playwright and Fetcher) combined with guided manual adjustments from the user.

## Input Data
- `product_context.json`
- `research_goals.json`
- `research_context.json`

## Collected Fields & Categorization
For each competitor, this skill initializes a profile containing:
- `id`: Unique string (e.g., `comp-stripe`).
- `name`: Competitor brand name.
- `website`: Competitor homepage URL.
- `category`: Must be one of the following:
  - `"Direct"`: Competitors serving the exact same target audience with a highly similar feature set (e.g. Stripe vs Paddle).
  - `"Indirect"`: Competitors solving the same core customer jobs/needs using a different mechanism or business model (e.g. Stripe vs a legacy bank manual wire transfer).
  - `"Best-in-class"`: Products that might not compete directly but represent the gold standard for specific interaction patterns or design systems we are researching (e.g. Linear for keyboard navigations).
  - `"Emerging"`: Newly launched or fast-growing platforms in the same space.
- `marketShare`: Qualitative assessment (e.g., `"Leader"`, `"Challenger"`, `"Niche"`, `"Newcomer"`).

---

## Execution Steps

### 1. Parse Parameters
- Read `product_context.json` to extract `productName`, `productCategory`, and `targetUsers`.
- Read `research_context.json` to check if the user specified pre-defined competitor URLs.

### 2. Auto-Discovery (If Competitors are not Pre-defined)
1. **Search Query Formulation**: Formulate standard query templates:
   - `Alternative to {{productCategory}}`
   - `Top {{productCategory}} software`
   - `Best tool for {{jobsToBeDone[0]}}`
2. **Scraping Directories**:
   - Use the `playwright` MCP to navigate search engines (e.g. Google) or software review directories (e.g. AlternativeTo, G2, Crunchbase).
   - Use the `fetcher` MCP to extract clean markdown/text content from search result listing pages.
3. **Extraction & Deduplication**: Parse listings to extract company names and homepage URLs. Deduplicate the list and select the top 3-5 candidates.

### 3. Manual Override Dialogue
1. Present the auto-discovered list to the user:
   > "I've discovered the following competitors: [List of names/URLs]. Do you want to approve this list, add manual URLs, or remove any entries?"
2. Accept the user's feedback to finalize the active competitor roster.

### 4. Categorize & Profile
For each competitor in the roster:
1. Fetch their homepage/landing page using `fetcher`.
2. Inspect their value proposition and features to assign their `category` ("Direct", "Indirect", "Best-in-class", "Emerging") and `marketShare` ("Leader", "Challenger", "Niche").
3. Set placeholder values for features, pricing, strengths, and weaknesses (to be completed by the competitor-analysis skill).

### 5. Save Roster
- Serialize the list of profiles and write it to `competitor_profiles.json` in the workspace root.

---

## Output Data
- Writes the generated array of objects to `competitor_profiles.json` in the workspace root.
