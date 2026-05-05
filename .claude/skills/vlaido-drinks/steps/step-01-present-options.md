# Step 1: Present Drink Options

Present 5 universal drinks or the option to skip drink

## Instructions

### 1. Check Existing Selection

Load `order_state.drink` from `{outputFile}`.

**If already set** (including "None"): Skip ahead → `../../vlaido-confirmation/SKILL.md`.

**If null**: Continue below.

### 2. Transition
Display : 

"Would you like to add a drink to your order?"

### 3. Present Menu
Display : 

"Here are our beverage options:

  **[1]** 💧 **Still Water** — Pure, refreshing still mineral water.
  **[2]** ✨ **Sparkling Water** — Crisp, effervescent sparkling mineral water.
  **[3]** 🍊 **Fresh Orange Juice** — Freshly squeezed orange juice, served chilled.
  **[4]** 🍷 **House Red Wine** — Our sommelier's selection — a smooth, medium-bodied red.
  **[5]** 🍵 **Mint Tea** — Fragrant fresh mint tea, a refreshing palate cleanser.

  **[0]** ❌ **No drink, thank you**

Enter a number (0–5), type the name, or say **skip**."

🛑 **HALT** — Wait for response.

### 4. Transition

Read fully and follow: `./step-02-confirm-selection.md`
