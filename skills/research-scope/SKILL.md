---
name: research-scope
description: Configure what interaction categories and UI components the agent will analyze during the competitor research.
---

# Research Scope Skill

This skill defines the scope of the competitor audit by allowing users to select specific interaction categories and UI components to analyze.

## Input Data
- Direct interactive user responses, or a pre-configured `research_scope.json` file in the workspace root.

## Predefined Analysis Categories
The user can select one or more categories from this standard list:

* **`Onboarding`**: Sign-up flow, email verifications, setup wizards, tour guides, and initial landing states.
* **`Navigation`**: Top navbar, side drawers, breadcrumbs, search-based navigation, footer links, and user settings menus.
* **`IA`**: Information Architecture, navigation hierarchy, sub-domain distribution, and URL patterns.
* **`Dashboard`**: Core user home screens, widget layouts, personalization modules, activity feeds, and data summaries.
* **`Search`**: Search input experience, auto-complete suggestions, global CMD+K bars, search results layouts, and zero-state guides.
* **`Filters`**: Category selectors, sidebar filters, date range picks, active tag chips, sort options, and multi-filter logic.
* **`Tables`**: Data list layouts, bulk actions, column customization, pagination, infinite scroll vs click-to-load, and inline editing.
* **`Forms`**: Input fields, inline validation error designs, tooltips, secure password constraints, dropdown selectors, and file upload components.
* **`AI`**: Conversational interfaces, AI summaries, text-to-code builders, smart actions, copilot modules, and prompt libraries.
* **`Collaboration`**: Multi-player editing cursors, comments, sharing links, team permission profiles, and workspace settings.
* **`Notifications`**: Bell dropdown lists, workspace activities, email digests, SMS alerts, system banners, and notification settings.
* **`Accessibility`**: Screen reader labels, keyboard tab navigation focus states, color contrast markers, and semantic markup tags.
* **`Pricing`**: Monthly vs annual toggle selectors, pricing cards, feature comparisons, checkouts, and billing settings.
* **`Mobile`**: App store links, responsive mobile web layouts, gesture-based actions, native bottom menus, and push alerts.

---

## Collected Fields & Validation Rules

The skill compiles and validates the following fields:

| Field | Type | Validation Rules | Description |
| :--- | :--- | :--- | :--- |
| `selectedCategories` | Array of Strings | Must contain at least 1 item. All items must exist in the Predefined list. | The target UI/UX areas of interest. |
| `customInstructions` | Object (Key-Value) | Keys must match selected categories. Values must be strings. | Specific design guidelines or details the user wants to audit for each category. |
| `deepInspect` | Object (Key-Value) | Keys must match selected categories. Values must be booleans. | Set to `true` if the agent should inspect element-level CSS/HTML parity (Figma design vs code). |

---

## Execution Steps

1. **Source Scope**: Check if `research_scope.json` exists in the workspace.
   - If found and valid, parse and load it.
   - If not found, run the interactive questionnaire in Step 2.
2. **Interactive Questionnaire**:
   - Present the predefined category checklist to the user.
   - Prompt: "Select the UX/UI categories you want to analyze (comma-separated list, e.g., Onboarding, Pricing):"
   - For each selected category, ask:
     - "Are there specific criteria or questions for {{category}}? (Leave empty for default analysis):"
     - "Do you want to run a deep CSS/design system token parity check for {{category}}? (yes/no):"
3. **Input Validation**: Validate entries against the schemas. Reject invalid category names.
4. **Serialize and Save**: Write the validated JSON object to the workspace root as `research_scope.json`.

## Output Data
- Write the validated structure to `research_scope.json` in the workspace root.
