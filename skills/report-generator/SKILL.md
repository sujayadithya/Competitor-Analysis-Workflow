---
name: report-generator
description: stitch and compile intermediate competitor JSON logs into unified Markdown and PDF reports, exporting via Playwright.
---

# Report Generation Skill

This skill loads all intermediate research data models and formats them into a polished, professional research report exported in both Markdown and PDF formats.

## Input Data
- `product_context.json`
- `research_goals.json`
- `research_scope.json`
- `competitor_profiles.json`
- `ux_patterns.json`
- `product_opportunities.json`
- Templates under `templates/`:
  - `report-template.md` (Main report structure)
  - `feature-matrix.md` (Features comparison layout)
  - `ux-pattern-library.md` (Screenshots & pattern detail layout)
  - `action-plan.md` (Prioritization & action items layout)

---

## Execution Steps

### 1. Load Data
1. Read all JSON profiles and context models from the workspace root.
2. Initialize variables for stitching templates.

### 2. Compile Report Sections
1. **Executive Summary**: Synthesize a high-level overview detailing the market position and key findings.
2. **Product Context**: Insert details from `product_context.json` (Name, Category, Overview, Persona targets, JTBD).
3. **Research Goals**: Insert goals and objectives from `research_goals.json`.
4. **Competitor Overview & Analysis**:
   - Loop through `competitor_profiles.json`.
   - Write sections for each competitor including website, category, market share, strengths, weaknesses, and positioning statements.
5. **Feature Matrix**:
   - Map competitor feature inventories into a side-by-side Markdown comparison table.
6. **UX Pattern Library**:
   - Loop through `ux_patterns.json`.
   - Populate screenshot image paths (using Markdown syntax and carousel tags) along with selectors, pros, cons, and best practice recommendations.
7. **Opportunity Analysis & Priorities**:
   - Render the prioritization matrix cards from `product_opportunities.json` showing impact and effort.
8. **Action Plan**:
   - Output checkbox lists of prioritized recommended actions.
9. **References**:
   - Include audited URLs, platform specifications, and timestamps.

### 3. Save Markdown Report
1. Stich all populated sub-templates into the base `report-template.md`.
2. Save the final file to `reports/competitor_research_report.md` using the `filesystem` MCP.

### 4. Export to PDF (Playwright Conversion)
1. Read the newly saved Markdown report.
2. Convert the Markdown file into a styled HTML document by wraping it in standard HTML tags and embedding a modern CSS stylesheet (defining Inter/Outfit fonts, sleek grid container boxes, and color tokens).
3. Launch a headless browser session using the `playwright` MCP.
4. Set the page content to the styled HTML document.
5. Call the browser page `pdf` function (setting parameters: A4 size, margins, print backgrounds) to save the rendered output to `reports/competitor_research_report.pdf`.

---

## Output Data
- Writes the Markdown report to `reports/competitor_research_report.md` in the workspace root.
- Writes the PDF report to `reports/competitor_research_report.pdf` in the workspace root.
