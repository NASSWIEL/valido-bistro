# Step 2: Final Confirmation

Process yes/no. If confirmed → finalize. If rejected → route to the item to change.

## Instructions

### 1. Validate Response

**Confirm:** `yes`, `y`, `yep`, `yeah`, `yup`, `confirm`, `confirmed`, `correct`, `looks good`, `looks great`, `perfect`, `ok`, `okay`, `sure`, `absolutely`, `go ahead`, `place the order`, `place it`

**Reject:** `no`, `n`, `nope`, `nah`, `change`, `changes`, `cancel`, `wrong`, `restart`, `start over`, `redo`, `not correct`, `incorrect`, `modify`, `edit`

**Invalid** (e.g., "maybe", "hmm", blank): Re-prompt with "Please reply **yes** to confirm or **no** to make changes." → HALT → loop.

### 2. On Confirmation → Finalize

Generate reference: `ORD-{year}-{random 1000–9999}`

Display:

"✅ **Order Confirmed!**

Thank you, {customer_name}! Your order has been placed.

🎫 **Order Reference:** `{reference}`

We're preparing:
- 🍽️ {main_course}
- 🍰 {dessert, omit line if None}

Your - 🥤 {drink, omit line if None} will be on your table within a minute

🍽️ *Bon appétit!*"

**Update state:**
- Set `order_state.order_reference` and `order_state.status` = `confirmed`
- Add `confirmation-step-02-final-confirmation` to `stepsCompleted`

Append:

```markdown

## ✅ Order Confirmation

**Status:** Confirmed
**Order Reference:** {reference}
**Confirmed At:** {current date and time}

| Item | Selection |
|---|---|
| Category | {category} |
| Main Course | {main_course} |
| Dessert | {dessert or 'No dessert'} |
| Drink | {drink or 'No drink'} |

---

*Thank you for dining with us at Vlaido Bistro!*
```

**Workflow ENDS.**

### 3. On Rejection → Ask What to Change

"Of course! What would you like to change?

  **[1]** 🏷️ **Category** — {category}
  **[2]** 🍽️ **Main Course** — {main_course}
  **[3]** 🍰 **Dessert** — {dessert or 'No dessert'}
  **[4]** 🥤 **Drink** — {drink or 'No drink'}
  **[A]** 🔄 **Start completely over**

Enter the number (1–4) or **A** to restart."

🛑 **HALT** — Wait for response.

### 4. Route the Change

| Input | Reset fields | Route to |
|---|---|---|
| `1`, `category` | category, main_course, main_course_description, dessert, dessert_description, drink → null | `../../vlaido-welcome/steps/step-02-category-selection.md` |
| `2`, `main course`, `main`, `dish` | main_course, main_course_description → null | `../../vlaido-main-course/steps/step-01-present-options.md` |
| `3`, `dessert`, `sweet` | dessert, dessert_description → null | `../../vlaido-dessert/steps/step-01-present-options.md` |
| `4`, `drink`, `beverage` | drink → null | `../../vlaido-drinks/steps/step-01-present-options.md` |
| `a`, `all`, `everything`, `start over`, `restart` | All selections → null (keep customer_name, language) | `../../vlaido-welcome/steps/step-02-category-selection.md` |

**Invalid**: Re-present change menu → HALT → loop.

**Before routing, execute the field resets listed above.** Update `order_state` in `{outputFile}` as follows:

- **[1] or category:** Set `order_state.category`, `order_state.main_course`, `order_state.main_course_description` = `null`
- **[2] or main course:** Set `order_state.main_course`, `order_state.main_course_description` = `null`
- **[3] or dessert:** Set `order_state.dessert`, `order_state.dessert_description` = `null`
- **[4] or drink:** Set `order_state.drink` = `null`

Only then proceed to display the acknowledgment and route.

Display a brief acknowledgment (e.g., "No problem! Let me show you the {category} main courses again.") then route.
