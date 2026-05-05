# Step 1: Present Dessert Options

Vegan category → vegan menu; others → standard. Include [0] skip option.

## Instructions

### 1. Check Existing Selection

Load `order_state.dessert` from `{outputFile}`.

**If already set** (including "None"): Skip ahead → `../../vlaido-drinks/SKILL.md`

**If null**: 

Display :

"Wonderful choice! You've selected: **{main_course}** — **{main_course_description}**. Now let's move on to dessert!"

### 2. Transition

"Wonderful! Now that your main course is settled, would you like to add a dessert?"

### 3. Present Menu

**If category is "Vegan":**

"Here are our vegan dessert selections:

  **[1]** 🍫 **Dark Chocolate Mousse** — Rich dark chocolate mousse with silken tofu and a hint of espresso.
  **[2]** 🥥 **Coconut Panna Cotta** — Silky coconut cream with passion fruit and mango coulis.
  **[3]** 🍨 **Mango Sorbet Trio** — Three vibrant sorbets — mango, raspberry, and lemon — with fresh mint.
  **[4]** 🥧 **Apple Crumble** — Warm spiced apple crumble with oat-almond topping and coconut cream.
  **[5]** 🍰 **Avocado Lime Cheesecake** — Raw cashew cheesecake with avocado and zesty lime.

  **[0]** ❌ **No dessert, thank you**

Enter a number (0–5), type the name, or say **skip**."

**All other categories:**

"Here are our dessert selections:

  **[1]** 🍰 **Tiramisu** — Classic mascarpone layers with espresso-soaked ladyfingers and cocoa.
  **[2]** 🍮 **Crème Brûlée** — Silky vanilla custard beneath caramelized sugar.
  **[3]** 🍫 **Chocolate Fondant** — Warm molten chocolate cake with vanilla bean ice cream.
  **[4]** 🍨 **Panna Cotta** — Delicate cream dessert with seasonal berry compote.
  **[5]** 🥧 **Tarte Tatin** — Caramelized apple tart with buttery pastry and Chantilly cream.

  **[0]** ❌ **No dessert, thank you**

Enter a number (0–5), type the name, or say **skip**."

🛑 **HALT** — Wait for response.

### 4. Transition

Read fully and follow: `./step-02-confirm-selection.md`
