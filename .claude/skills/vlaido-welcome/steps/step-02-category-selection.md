# Step 2: Dietary Category Selection

Present 5 dietary categories, validate, transition to main course.

## Instructions

### 1. Present Options

"Now, please select your preferred dining category:

  **[1]** 🥩 Beef
  **[2]** 🐟 Fish
  **[3]** 🥗 Vegetarian
  **[4]** 🌱 Vegan
  **[5]** 👨‍🍳 Chef's Special

Please enter the number (1–5) or type the category name."

🛑 **HALT** — Wait for response.

### 2. Validate

| Input | Category |
|---|---|
| `1`, `beef` | Beef |
| `2`, `fish` | Fish |
| `3`, `vegetarian`, `veggie`, `veg` | Vegetarian |
| `4`, `vegan` | Vegan |
| `5`, `chef`, `chef's special`, `chefs special`, `secret` | Chef's Special |

- Number or name/alias match (case-insensitive) → valid
- Unambiguous partial (e.g., "bee" → Beef) → valid
- Otherwise → INVALID: polite re-prompt → re-present options → HALT

### 3. Confirm

"Excellent choice! You've selected: **{category}**. Let me show you our **{category}** main courses."

### 4. Update State

- Set `order_state.category`
- Add `step-02-category-selection` to `stepsCompleted`

Append:

```markdown

## 📋 Category Selection

**Selected Category:** {category}

---
```

### 5. Transition

Read fully and follow: `../../vlaido-main-course/SKILL.md`
