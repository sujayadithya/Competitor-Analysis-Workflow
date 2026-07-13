---
name: competitor-discovery
description: Discover and list primary market competitors based on target parameters and project focus areas.
---

# Competitor Discovery Skill

This skill searches public search engines, app stores, and industry databases to discover competitor products matching the research context.

## Input Data
- `research_context.json`

## Execution Steps
1. Parse `research_context.json` to extract goals, focus areas, and target audience.
2. Build search queries targeting keywords, platforms, and segment classifications.
3. Call the `fetcher` or `playwright` tool to query search directories and fetch competitor homepage URLs.
4. Filter out non-competitor resources (such as blogs, news sites, or reviews) to maintain a maximum list of 5 direct competitors.
5. Create initial `CompetitorProfile` JSON structures for each discovered competitor.

## Output Data
- Write the list of profiles to `competitor_profiles.json`.
