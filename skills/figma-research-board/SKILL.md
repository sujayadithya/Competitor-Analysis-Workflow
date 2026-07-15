---
name: figma-research-board
description: Connect to Figma, create pages/frames, organize screenshot assets, and lay out annotations/opportunity sticky notes on a canvas.
---

# Figma Research Board Skill

This skill transforms structured competitor analysis, opportunity priorities, and visual screenshot assets into an organized visual research board directly on a Figma design canvas.

## Input Data
- `product_context.json`
- `competitor_profiles.json`
- `ux_patterns.json`
- `product_opportunities.json`
- `config/settings.json` (specifying Figma target file / canvas nodes if predefined)

---

## Target Canvas structure

The skill creates a structured visual hierarchy on the Figma canvas:

```text
Figma File / Page: Competitor Analysis Research Board
└── Root Frame [Width: 6000px, Height: 4000px]
    ├── Title Block (Header, Metadata, Focus Areas)
    ├── Opportunities Panel (Prioritized cards linking to flows)
    └── Competitor Columns (Dynamic sections for each audited brand)
        ├── Direct / Indirect Categorization headers
        └── UX Category Rows (Navigation, Dashboard, Forms, AI, etc.)
            ├── Captured Screenshot Nodes (fitted with image fills)
            └── Callout Sticky Notes (Green for Pros, Red for Cons, Yellow for Opps)
```

---

## Execution Steps

### 1. Establish Connection & Initialize Board
1. Call the `figma-console/figma_get_status` tool to check for active open files.
2. Verify that `valid` is `true` and a `currentFileKey` is returned. If not, prompt the user to open a Figma desktop file with the plugin active.
3. Call `figma_create_child` to generate the root Frame node (`"Competitor Analysis Research Board"`) on the canvas coordinate `(0, 0)`.

### 2. Populate Header & Opportunities Panel
1. Call `figma_create_child` to insert text nodes for the Project Name, Date, and Target Audience.
2. Read `product_opportunities.json`. For each opportunity:
   - Create a rectangular card container with a light background.
   - Insert text detailing the priority (P0/P1), title, gap addressed, and action plan.
   - Place these cards in a vertical row on the left side of the Root Frame.

### 3. Build Competitor Auditing Columns
Read `competitor_profiles.json` and `ux_patterns.json` to draw the matrix:
1. **Competitor Columns**: Loop through each competitor. Calculate an X-coordinate offset (e.g., `X = 500 + competitorIndex * 1500`) to place their column.
2. **Category Rows**: Loop through the selected categories from `research_scope.json` (or the predefined list in `ux_patterns.json`). Calculate a Y-coordinate offset (e.g., `Y = 300 + categoryIndex * 800`).
3. **Insert Screenshots**:
   - Create a rectangle frame (e.g., `width: 800`, `height: 500`).
   - Call `figma_set_image_fill` to upload the corresponding screenshot (from `assets/screenshots/`).
4. **Attach Annotations (Sticky Notes)**:
   - Create small colored squares next to the screenshot (e.g., `width: 200`, `height: 200`).
   - Use green fills for **Pros**, red fills for **Cons**, and yellow fills for **Opportunities**.
   - Call `figma_set_text` to write the qualitative observation text inside the sticky note.

### 4. Arrange & Group
1. Call `figma_arrange_component_set` or adjust positioning coordinates (`figma_move_node`) to ensure columns, rows, images, and notes are clean and perfectly aligned.
2. Return a summary report listing the total nodes created and a direct Figma link to the generated frame.

---

## Output Data
- Modifies the live Figma file canvas.
- Returns a completion log with node IDs and coordinate maps.
