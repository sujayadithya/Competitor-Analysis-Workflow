---
name: report-generator
description: Generate a structured competitor research report in markdown or PDF format utilizing templates and captured assets.
---

# Report Generator Skill

This skill compiles all data models and assets into a professional research report.

## Input Data
- `research_context.json`
- `competitor_profiles.json`
- `ux_patterns.json`
- `product_opportunities.json`
- templates in the `templates/` directory

## Execution Steps
1. Parse the research results and populate the base markdown structures defined under `templates/`.
2. Format a side-by-side feature comparison table.
3. Build a visual UX Pattern Library displaying screenshot assets and interaction notes.
4. Present the prioritized Product Opportunity Matrix and action plans.
5. Save the generated file under `reports/competitor_research_report.md`.

## Output Data
- Write the final report markdown file.
