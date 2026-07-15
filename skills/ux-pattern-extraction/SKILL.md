---
name: ux-pattern-extraction
description: Crawl competitor interfaces, trigger key UI states, capture screenshots, and extract reusable design patterns for the UX Pattern Library.
---

# UX Pattern Extraction Skill

This skill automates the extraction and categorization of reusable UX patterns across competitors, capturing visual evidence and interaction details.

## Input Data
- `research_context.json`
- `research_scope.json`
- `competitor_profiles.json`

## Audit States & Interactive Flow Categories
This skill audits interaction flows and captures distinct states under these categories:

1. **`Navigation`**: Persistent menus, sidebar behaviors, headers, responsive hamburger toggles.
2. **`Search`**: Focus inputs, CMD+K bar triggers, instant results dropdowns, zero-state behaviors.
3. **`Filters`**: Multi-select filters, active filter chips, tag sorting, inline date range pickers.
4. **`Tables`**: Bulk select boxes, row hover interactions, infinite scroll skeletons, column customization triggers.
5. **`Dashboards`**: Grid layouts, widget personalization modals, collapsible charts, drag-and-drop actions.
6. **`Forms`**: Input focuses, helper tooltips, inline password show/hide CTAs, select boxes.
7. **`Empty States`**: Interfaces displaying missing data (e.g. empty inbox, fresh project view).
8. **`Loading`**: Skeleton overlays, inline spinners, progress indicators during data fetches.
9. **`Errors`**: Inline validation alerts, toast banners, form submission blockers, failure limits.
10. **`Permissions`**: Cookie consent banners, secure OAuth popups, profile roles restrictions.
11. **`Notifications`**: Bell list dropdowns, system toast banners, floating banner dismissals.
12. **`AI`**: Conversational chat inputs, inline copy/regenerate pills, AI badge indicators.

---

## Execution Steps

### 1. Formulate Targets
- Read `research_scope.json` to identify active UI/UX categories.
- Read `competitor_profiles.json` to extract competitor login, landing, and dashboard URLs.

### 2. Automate User Flow Audits (Playwright & Figma)
For each selected UI category and competitor:
1. **Initialize Session**: Launch a Playwright browser session.
2. **Navigate & Auditing**:
   - Navigate to the entry point page for the selected category.
   - Run specific actions (click, scroll, type) to trigger interactive states:
     - *To test Forms/Errors*: Submit invalid inputs.
     - *To test Empty States*: Navigate to an empty resource folder or table.
     - *To test Loading*: Throttle networks or trigger API calls to capture spinners.
3. **Capture Evidence**:
   - Take element-specific or viewport-specific screenshots of the active states.
   - Save screenshots to `assets/screenshots/competitor-{{name}}-{{category}}-{{state}}.png`.
   - Record CSS layout tokens and DOM element selectors (e.g., `#signup-form input.error`).

### 3. Parse Reusable Patterns
Analyze the flow to extract the following attributes:
- **Pros**: Interaction design successes (e.g. "Auto-focus code input saves key clicks").
- **Cons**: Flow friction points (e.g. "Redirection during OAuth breaks flow continuity").
- **Best Practices**: Pattern recommendations to apply to our design system.
- **Design System Parity**: Review typography, color spacing tokens, and note compliance details.

### 4. Write UX Pattern Library
- Formulate a JSON array of `UXPattern` objects.
- Write this data structure to `ux_patterns.json` in the workspace root.

---

## Output Data
- Writes the structured array of UX patterns to `ux_patterns.json` in the workspace root.
