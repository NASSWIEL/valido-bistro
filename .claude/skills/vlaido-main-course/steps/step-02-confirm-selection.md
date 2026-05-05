# Step 2: Confirm Main Course Selection

Validate dish selection and transition to dessert.

## Instructions

### 1. Matching Rules by Category

Load `order_state.category` from `{outputFile}` and use the corresponding table:

**Beef:**

| Input | Dish | Description |
|---|---|---|
| `1`, `ribeye`, `grilled ribeye`, `grilled ribeye steak` | Grilled Ribeye Steak | Chargrilled 300g ribeye with herb butter, roasted garlic, and hand-cut fries |
| `2`, `bourguignon`, `beef bourguignon` | Beef Bourguignon | Slow-braised beef in red wine with pearl onions, mushrooms, and buttery mash |
| `3`, `filet`, `filet mignon`, `mignon` | Filet Mignon | Pan-seared tenderloin with truffle demi-glace, asparagus, and dauphinoise potatoes |
| `4`, `tagliata`, `beef tagliata` | Beef Tagliata | Sliced sirloin over wild rocket with aged parmesan and balsamic reduction |
| `5`, `short ribs`, `braised short ribs` | Braised Short Ribs | 8-hour braised short ribs with creamy polenta and citrus gremolata |

**Fish:**

| Input | Dish | Description |
|---|---|---|
| `1`, `salmon`, `pan-seared salmon` | Pan-Seared Salmon | Atlantic salmon fillet with lemon-dill sauce and sautéed spinach |
| `2`, `sea bass`, `grilled sea bass` | Grilled Sea Bass | Whole Mediterranean sea bass with cherry tomatoes, capers, and olive oil |
| `3`, `tuna`, `seared tuna`, `tuna steak` | Seared Tuna Steak | Rare-seared yellowfin tuna with wasabi crust and soy-ginger glaze |
| `4`, `lobster`, `lobster thermidor`, `thermidor` | Lobster Thermidor | Half lobster gratinated with mustard cream and gruyère cheese |
| `5`, `cod`, `cod en papillote` | Cod en Papillote | Oven-baked cod fillet with fennel, citrus, and white wine in parchment |

**Vegetarian:**

| Input | Dish | Description |
|---|---|---|
| `1`, `risotto`, `mushroom risotto`, `wild mushroom risotto` | Wild Mushroom Risotto | Creamy Arborio rice with porcini, shiitake, and truffle oil |
| `2`, `parmigiana`, `eggplant`, `eggplant parmigiana` | Eggplant Parmigiana | Layered eggplant with fresh mozzarella, basil, and San Marzano tomato sauce |
| `3`, `peppers`, `stuffed peppers`, `stuffed bell peppers` | Stuffed Bell Peppers | Roasted peppers filled with quinoa, feta, and toasted pine nuts |
| `4`, `ravioli`, `spinach ravioli`, `spinach and ricotta ravioli` | Spinach and Ricotta Ravioli | Handmade pasta parcels in sage brown butter sauce |
| `5`, `wellington`, `vegetable wellington` | Vegetable Wellington | Golden puff pastry with seasonal roasted vegetables and goat cheese |

**Vegan:**

| Input | Dish | Description |
|---|---|---|
| `1`, `cauliflower`, `cauliflower steak` | Cauliflower Steak | Roasted cauliflower with chimichurri, smoked paprika, and toasted almonds |
| `2`, `curry`, `thai curry`, `thai green curry`, `green curry` | Thai Green Curry | Fragrant coconut curry with crispy tofu, bamboo shoots, and jasmine rice |
| `3`, `beetroot`, `beetroot carpaccio`, `carpaccio` | Beetroot Carpaccio | Thinly sliced roasted beetroot with avocado, walnut, and citrus dressing |
| `4`, `portobello`, `stuffed portobello`, `mushroom` | Stuffed Portobello Mushroom | Grilled portobello cap with herb couscous and roasted red peppers |
| `5`, `moussaka`, `lentil moussaka` | Lentil Moussaka | Layers of spiced lentils, eggplant, and potato with cashew béchamel |

**Chef's Special:**

| Input | Dish | Description |
|---|---|---|
| `1`, `duck`, `duck confit`, `confit` | Duck Confit | Slow-cooked duck leg with cherry reduction and dauphinoise potatoes |
| `2`, `lamb`, `rack of lamb` | Rack of Lamb | Herb-crusted lamb with rosemary jus and Provençal ratatouille |
| `3`, `truffle`, `truffle pasta`, `pasta` | Truffle Pasta | Fresh tagliatelle with shaved black truffle, parmesan cream, and wild arugula |
| `4`, `paella`, `seafood paella` | Seafood Paella | Saffron rice with king prawns, mussels, squid, and Spanish chorizo |
| `5`, `wagyu`, `wagyu burger`, `burger` | Wagyu Burger | Premium wagyu patty with foie gras, caramelized onion, and toasted brioche bun |

**Matching:** Number match → valid. Case-insensitive name/alias → valid. Unambiguous partial → valid. Otherwise → INVALID.

### 2. Handle Invalid Input

Re-present the category's dish options with: "I didn't catch that. Could you choose one of these dishes?"

🛑 **HALT** — Wait for new response. Loop until valid.

### 3. Confirm

"Wonderful choice! You've selected: **{dish}** — {description}. Now let's move on to dessert!"

### 4. Update State

- Set `order_state.main_course` and `order_state.main_course_description`
- Add `main-course-step-02-confirm-selection` to `stepsCompleted`

**Find the existing `## 🍽️ Main Course` section in `{outputFile}` and update it in place.** If no such section exists yet, append it.

```markdown

## 🍽️ Main Course

**Category:** {category}
**Selected Dish:** {dish}
**Description:** {description}

---
```

### 5. Transition

Read fully and follow: `../../vlaido-dessert/SKILL.md`
