---
name: ux-pattern-extraction
description: Capture visual screenshots, extract user flows, and identify interaction patterns across competitor web/app interfaces.
---

# UX Pattern Extraction Skill

This skill uses automated browser scripts via Playwright or inspections via Figma to capture screenshots of user flows and document interaction details.

## Input Data
- `research_context.json`
- `competitor_profiles.json`

## Execution Steps
1. Parse the focus areas/user flows requested in `research_context.json` (e.g. signup flow).
2. For each competitor in `competitor_profiles.json`:
   - Initialize browser automation using the `playwright` MCP.
   - Programmatically navigate to the entry screen of the target flow.
   - Walk through the user flow steps, taking high-resolution screenshots at each key step.
   - Save screenshots to `assets/screenshots/` following a standard naming scheme.
   - Extract and document interactive elements (selectors, fields, CTA copy, verification details).
   - Evaluate accessibility and design consistency.
3. Formulate `UXPattern` objects linking to the captured screenshots and describing each step.

## Output Data
- Write the list of patterns to `ux_patterns.json`.
