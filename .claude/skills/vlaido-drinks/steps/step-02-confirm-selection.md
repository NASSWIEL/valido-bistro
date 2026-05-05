# Step 2: Confirm Drink Selection

Validate drink selection or skip, then transition to confirmation.

## Instructions

### 1. Skip Detection (CHECK FIRST)

If input matches: `0`, `no`, `none`, `skip`, `no drink`, `no drinks`, `no thanks`, `i'm good`, `im good`, `pass`, `nothing`, `no beverage` → go to instruction 4.

### 2. Matching Rules

| Input | Drink |
|---|---|
| `1`, `still water`, `still` | Still Water |
| `2`, `sparkling water`, `sparkling`, `fizzy water`, `soda water` | Sparkling Water |
| `3`, `orange juice`, `fresh orange juice`, `juice`, `oj` | Fresh Orange Juice |
| `4`, `red wine`, `house red`, `house red wine`, `wine` | House Red Wine |
| `5`, `mint tea`, `tea`, `mint` | Mint Tea |

**Ambiguity — just `water`:** Do NOT default. Ask: "Would you prefer **Still Water** or **Sparkling Water**?" → HALT → validate clarification.

**Invalid**: Re-present options with polite message → HALT → loop.

### 3. Confirm Selection

"Great choice! You've selected: **{drink}**. We're almost done — let me prepare your order summary!"

### 4. Handle Skip

"No problem! We'll skip the drink. Let me prepare your order summary!"

Set `drink` = `None`.

### 5. Update State

- Set `order_state.drink`
- Add `drinks-step-02-confirm-selection` to `stepsCompleted`

**Find the existing `## 🥤 Drink` section in `{outputFile}` and update it in place.** If no such section exists yet, append it.

```markdown

## 🥤 Drink

**Selected Drink:** {drink}

---
```

### 6. Transition

Read fully and follow: `../../vlaido-confirmation/SKILL.md`
