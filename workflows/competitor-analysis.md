# Competitor Analysis Workflow Orchestrator

This document orchestrates the end-to-end competitor analysis process. It guides Antigravity through input collection, data modeling, sequential skill execution, and final report generation.

---

## 📋 Execution Protocol

### Step 1: Initialize Product Context
1. Execute [product-context/SKILL.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/skills/product-context/SKILL.md) to gather and validate details about the user's own product.
2. Save the result to the workspace root as `product_context.json` (matching the `ProductContext` schema in [docs/architecture.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/docs/architecture.md)).

---

### Step 2: Initialize Research Goals & Objectives
1. Execute [research-goals/SKILL.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/skills/research-goals/SKILL.md) to capture, validate, and prioritize the research goals and specific questions.
2. Save the result to the workspace root as `research_goals.json` (matching the `ResearchGoals` schema in [docs/architecture.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/docs/architecture.md)).

---

### Step 3: Initialize Research Context
1. Prompt the user with the Guided Questionnaire defined in [workflow.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/docs/workflow.md).
2. Process the user's answers and create the `ResearchContext` JSON object (matching the schema in [architecture.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/docs/architecture.md)).
3. Write this object to the scratch workspace folder as `research_context.json`.

---

### Step 4: Discover Competitors
1. Read `product_context.json`, `research_goals.json`, and `research_context.json`.
2. Execute [competitor-discovery/SKILL.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/skills/competitor-discovery/SKILL.md) to generate a list of primary competitors.
3. Save the result to the workspace as `competitor_profiles.json` (as a list of `CompetitorProfile` models).

---

### Step 5: Analyze Competitor Features & Pricing
1. Read `competitor_profiles.json`.
2. Execute [competitor-analysis/SKILL.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/skills/competitor-analysis/SKILL.md) to inspect competitor websites, fill in pricing details, list key features, and evaluate strengths/weaknesses.
3. Overwrite `competitor_profiles.json` with the enriched competitor profiles.

---

### Step 6: Extract UX Patterns & Capture Evidence
1. Read `research_context.json` and the enriched `competitor_profiles.json`.
2. Execute [ux-pattern-extraction/SKILL.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/skills/ux-pattern-extraction/SKILL.md) to launch Playwright or connect to Figma.
3. For each competitor, navigate through the target focus flows (e.g. signup, onboarding), capture step-by-step screenshot evidence, and log the HTML element selectors.
4. Save screenshots under `assets/screenshots/` (with file names matching the convention `competitor-{name}-{flow}-{step}.png`).
5. Write the extracted data to the workspace as `ux_patterns.json` (matching the `UXPattern` schema).

---

### Step 7: Perform Opportunity Analysis
1. Read `product_context.json`, `research_goals.json`, `competitor_profiles.json`, and `ux_patterns.json`.
2. Execute [opportunity-analysis/SKILL.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/skills/opportunity-analysis/SKILL.md) to identify feature gaps, evaluate UX patterns against design system parity, and detect product opportunities.
3. Save the output to the workspace as `product_opportunities.json` (matching the `ProductOpportunity` schema).

---

### Step 8: Generate Structured Report
1. Read all generated JSON models:
   - `product_context.json`
   - `research_goals.json`
   - `research_context.json`
   - `competitor_profiles.json`
   - `ux_patterns.json`
   - `product_opportunities.json`
2. Execute [report-generator/SKILL.md](file:///Users/sujay/Documents/App%20Projects/Competitor%20Analysis%20Workflow/skills/report-generator/SKILL.md) using formatting templates under `templates/` (e.g. `report-template.md`, `feature-matrix.md`, `ux-pattern-library.md`, and `action-plan.md`).
3. Compile and save the final report under `reports/competitor_research_report.md`.
4. Render the compiled markdown file for the user to review.
