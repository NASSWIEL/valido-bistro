# Step 2: Confirm Dessert Selection

Validate dessert selection or skip, then transition to drinks.

## Instructions

### 1. Skip Detection (CHECK FIRST)

If input matches: `0`, `no`, `none`, `skip`, `no dessert`, `no thanks`, `i'm good`, `im good`, `pass`, `nothing` → go to instruction 4.

### 2. Matching Rules

Load `order_state.category` to determine table.

**Vegan desserts:**

| Input | Dessert | Description |
|---|---|---|
| `1`, `mousse`, `chocolate mousse`, `dark chocolate mousse` | Dark Chocolate Mousse | Rich dark chocolate mousse with silken tofu and a hint of espresso |
| `2`, `coconut panna cotta`, `coconut`, `panna cotta` | Coconut Panna Cotta | Silky coconut cream with passion fruit and mango coulis |
| `3`, `sorbet`, `mango sorbet`, `mango` | Mango Sorbet Trio | Three vibrant sorbets — mango, raspberry, and lemon — with fresh mint |
| `4`, `crumble`, `apple crumble`, `apple` | Apple Crumble | Warm spiced apple crumble with oat-almond topping and coconut cream |
| `5`, `cheesecake`, `avocado cheesecake`, `lime cheesecake` | Avocado Lime Cheesecake | Raw cashew cheesecake with avocado and zesty lime |

**Standard desserts (all other categories):**

| Input | Dessert | Description |
|---|---|---|
| `1`, `tiramisu` | Tiramisu | Classic mascarpone layers with espresso-soaked ladyfingers and cocoa |
| `2`, `creme brulee`, `crème brûlée`, `brulee` | Crème Brûlée | Silky vanilla custard beneath caramelized sugar |
| `3`, `fondant`, `chocolate fondant`, `chocolate` | Chocolate Fondant | Warm molten chocolate cake with vanilla bean ice cream |
| `4`, `panna cotta`, `pannacotta`, `panna` | Panna Cotta | Delicate cream dessert with seasonal berry compote |
| `5`, `tarte tatin`, `tarte`, `tatin`, `apple tart` | Tarte Tatin | Caramelized apple tart with buttery pastry and Chantilly cream |

**Invalid**: Re-present options with polite message → HALT → loop.

### 3. Confirm Selection

"Lovely choice! You've selected: **{dessert}** — {description}. Now let's pick a drink!"

### 4. Handle Skip

"No problem! We'll skip dessert. Let's move on to drinks."

Set `dessert` = `None`, `description` = `Customer chose to skip dessert`.

### 5. Update State

- Set `order_state.dessert` and `order_state.dessert_description`
- Add `dessert-step-02-confirm-selection` to `stepsCompleted`

**Find the existing `## 🍰 Dessert` section in `{outputFile}` and update it in place.** If no such section exists yet, append it.

```markdown

## 🍰 Dessert

**Selected Dessert:** {dessert}
**Description:** {description}

---
```

### 6. Transition

Read fully and follow: `../../vlaido-drinks/SKILL.md`
