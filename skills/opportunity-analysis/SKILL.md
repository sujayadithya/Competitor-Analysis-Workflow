---
name: opportunity-analysis
description: Synthesize competitor profiles and UX patterns to identify feature gaps, detect emerging trends, formulate optimized user flows, and compile prioritized action plans.
---

# Opportunity & Recommendation Skill

This skill analyzes competitor data and UX patterns to isolate product opportunities, recommend best-practice design flows, outline emerging market trends, and formulate prioritizations.

## Input Data
- `product_context.json`
- `research_goals.json`
- `research_scope.json`
- `competitor_profiles.json`
- `ux_patterns.json`

## Collected Fields & Schema Extensions
This skill outputs a list of structured objects matching the extended `ProductOpportunity` schema, containing:
- `id`: Unique string (e.g. `opp-custom-auth-link`).
- `title`: Short name of the product opportunity.
- `description`: Detailed description of the recommendation.
- `gapAddressed`: Specific feature gap or UX friction point resolved by this opportunity.
- `competitorsImpacted`: Array of competitor names that offer or lack this capability.
- `opportunityType`: `"Feature Gap"` | `"UX Improvement"` | `"Pricing Strategy"` | `"Technology Advantage"`.
- `impact`: `"High"` | `"Medium"` | `"Low"`.
- `effort`: `"High"` | `"Medium"` | `"Low"`.
- `actionPlan`: Array of clear development tasks to build it.
- `bestPerformingPatterns`: Array of objects referencing competitor UX patterns:
  - `competitorName`: Name of competitor.
  - `patternId`: ID of reference pattern in `ux_patterns.json`.
  - `rationale`: Rationale why this specific pattern represents a best practice.
- `recommendedFlowSteps`: Array of step descriptions outlining the optimized recommended user flow.
- `emergingTrends`: Array of trend terms or summaries observed across competitors.

---

## Execution Steps

### 1. Load Inputs
1. Read all JSON profiles and context models (`product_context.json`, `research_goals.json`, `research_scope.json`, `competitor_profiles.json`, `ux_patterns.json`).

### 2. Synthesize Feature Gap Matrix
1. Extract the audited features for each competitor from their `featureInventory`.
2. Construct a pivot comparison matrix mapping selected categories (from `research_scope.json`) to competitor support status (`Supported` | `Partial` | `Unsupported`).
3. Identify categories where most competitors are `"Unsupported"` or `"Partial"`, highlighting these as market gap opportunities.

### 3. Evaluate Best-Performing UX Patterns
1. Audit the `ux_patterns.json` objects.
2. Read the `patternPros` and `patternCons` lists for each competitor flow.
3. Select patterns with the highest pros and minimal cons. Link these as best-practice references (`bestPerformingPatterns`).

### 4. Formulate Recommended User Flows
1. Combine the best-practice steps from competitor patterns into an optimized, unified user flow.
2. Draft the step-by-step sequence for our own product in `recommendedFlowSteps`.

### 5. Spot Emerging Trends
1. Review the `observations` and `notes` columns in the competitor profiles.
2. Extract common technical choices (e.g. usage of WebAuthn, AI prompt helpers, inline VAT validation) and log them under `emergingTrends`.

### 6. Prioritize Opportunities (Impact vs. Effort Matrix)
For each identified opportunity, evaluate:
- **Impact**: High (improves target success metrics >20% or fills P0 gap) | Medium | Low.
- **Effort**: High (requires backend architecture overhauls) | Medium | Low.
- **Priority Recommendation**:
  - *High Impact + Low Effort* ➡️ **P0 (Quick Wins)**
  - *High Impact + Medium/High Effort* ➡️ **P1 (Strategic Goals)**
  - *Medium/Low Impact + Low/Medium Effort* ➡️ **P2 (Nice-to-Haves)**

### 7. Compile Action Plans
1. Define 2-4 granular execution tasks under `actionPlan` to transition from research to code.
2. Serialize the array of opportunities and write to `product_opportunities.json` in the workspace root.

---

## Output Data
- Writes the structured opportunities list to `product_opportunities.json` in the workspace root.
