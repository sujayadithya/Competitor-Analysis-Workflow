---
name: opportunity-analysis
description: Analyze competitor gaps, evaluate UX design system parity, and identify product development opportunities.
---

# Opportunity Analysis Skill

This skill synthesizes data from competitor profiles and extracted UX patterns to highlight product gaps, evaluate design consistency, and list product opportunities.

## Input Data
- `competitor_profiles.json`
- `ux_patterns.json`

## Execution Steps
1. Compare feature matrix columns across all competitors to identify empty cells (feature gaps).
2. Contrast competitor UX steps (e.g. friction points, signup steps) to identify design improvements.
3. Review design system parity (fonts, colors, alignment) to identify where standard patterns are broken or excelled at.
4. Formulate `ProductOpportunity` objects containing recommended opportunities, effort-impact matrix, and action plans.

## Output Data
- Write the list of opportunities to `product_opportunities.json`.
