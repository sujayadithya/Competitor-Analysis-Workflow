---
name: research-goals
description: Capture raw research requirements, transform them into prioritized objectives, and define target questions.
---

# Research Goals Skill

This skill translates high-level stakeholder research ambitions into structured, actionable research objectives and questions to focus the scraping and UX analysis.

## Input Data
- Direct interactive user responses, or a pre-configured `research_goals.json` file in the workspace root.

## Collected Fields & Validation Rules
The skill collects and structures the following fields:

### 1. Raw Goals (`rawGoals`)
- **Type**: Array of Strings
- **Validation**: Minimum 1 item, each item must be at least 15 characters long.

### 2. Research Objectives (`researchObjectives`)
An objective is a refined goal mapped to concrete questions.
- **`objectiveId`**: Alphanumeric ID (e.g., `obj-pricing-transparency`).
- **`description`**: A concise action statement (e.g., "Analyze how transparently competitors present their fees").
- **`priority`**: Must be `"High"`, `"Medium"`, or `"Low"`.
- **`targetQuestions`**: Array of Strings (minimum 1 item). Specific questions the research must answer (e.g., "Are setup fees mentioned before signup?").

### 3. Focus Prioritization (`focusPrioritization`)
A mapping dividing focus features or interaction areas into priority categories:
- **`highPriority`**: Array of Strings (e.g., `["onboarding", "billing"]`)
- **`mediumPriority`**: Array of Strings
- **`lowPriority`**: Array of Strings

## Execution Steps
1. **Source Goals**: Check if a `research_goals.json` file exists in the workspace.
   - If found and valid, parse and load it.
   - If not found, trigger the interactive questionnaire in Step 2.
2. **Goal Refinement Dialogue**:
   - Prompt the user: "What are your primary goals for this competitor analysis?"
   - For each raw goal, ask:
     - "How would you state this as a clear research objective?"
     - "What specific questions do you want answered about this?"
     - "What is the priority for this objective (High/Medium/Low)?"
3. **Prioritize Interactions**:
   - Prompt the user to assign focus interaction flows (e.g., checkout, signup, dashboard) into High, Medium, or Low priorities.
4. **Input Validation**: Validate fields against the schemas. If any check fails, prompt the user for clarification.
5. **Serialize and Save**: Write the structured JSON object to the workspace root as `research_goals.json`.

## Output Data
- Write the validated structure to `research_goals.json` in the workspace root.
