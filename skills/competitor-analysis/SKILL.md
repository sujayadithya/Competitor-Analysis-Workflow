---
name: competitor-analysis
description: Perform deep analysis of discovered competitors, identifying pricing models, feature offerings, and strengths/weaknesses.
---

# Competitor Analysis Skill

This skill scrapes and analyzes competitor websites to extract qualitative and quantitative details about their business and product offerings.

## Input Data
- `competitor_profiles.json` (initial profiles)
- `research_context.json`

## Execution Steps
1. Read the competitor list from `competitor_profiles.json`.
2. Use the `fetcher` tool to scrape each competitor's homepage, pricing page, and features page.
3. Identify pricing tiers, subscription models, features included in each plan, and general value propositions.
4. Synthesize competitor strengths, weaknesses, and market positioning relative to the project goals.
5. Enrich each profile in `competitor_profiles.json` with the extracted data.

## Output Data
- Overwrite `competitor_profiles.json` with the enriched list of profiles.
