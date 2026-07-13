---
name: product-context
description: Gather, validate, and store context about the user's own product to establish a research baseline.
---

# Product Context Skill

This skill captures and documents the key characteristics of the user's product to establish the baseline criteria for competitor comparison.

## Input Data
- Direct interactive user responses, or a pre-configured `product_context.json` file in the workspace root.

## Collected Fields & Validation Rules
The skill collects the following fields, validating them against the specified rules:

| Field | Type | Validation Rules | Description |
| :--- | :--- | :--- | :--- |
| `productName` | String | Must be non-empty, max 100 characters. | The name of the user's product. |
| `productCategory` | String | Must be non-empty, alphanumeric and spaces. | General market sector or category. |
| `productOverview` | String | Must be non-empty, minimum 50 characters. | High-level summary of the product's value. |
| `targetUsers` | Array of Strings | Must contain at least 1 non-empty item. | The primary user personas or target segments. |
| `jobsToBeDone` | Array of Strings | Must contain at least 1 non-empty item. | Core customer needs/tasks (JTBD framework). |
| `businessGoals` | Array of Strings | Must contain at least 1 non-empty item. | Success targets for the business. |
| `challenges` | Array of Strings | Must contain at least 1 non-empty item. | Key friction points or problems being solved. |
| `successMetrics` | Array of Strings | Must contain at least 1 non-empty item. | Metrics used to measure product success. |

## Execution Steps
1. **Source Context**: Check if a `product_context.json` file exists in the workspace root.
   - If the file exists and is valid, parse and load it.
   - If the file does not exist, trigger the interactive questionnaire in Step 2.
2. **Interactive Questionnaire**: Prompt the user to answer the questions for each collected field sequentially.
3. **Input Validation**: 
   - Check each input against the Validation Rules.
   - If any validation fails, explain the error and prompt the user to re-input the value.
4. **Serialize and Save**: Write the validated JSON object to the workspace root as `product_context.json`.

## Output Data
- Write the validated product profile structure to `product_context.json` in the workspace root.
