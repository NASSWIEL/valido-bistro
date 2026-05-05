# Step 1: Present Main Course Options

Present 5 dishes matching `order_state.category`. Do not validate here — that is step 2.

## Instructions

### 1. Load Category

Read `order_state.category` from `{outputFile}`. If null/missing → redirect to `../../vlaido-welcome/steps/step-02-category-selection.md`.

### 2. Present Menu

**Beef:**

"Here are our finest Beef dishes:

  **[1]** 🥩 **Grilled Ribeye Steak** — Chargrilled 300g ribeye with herb butter, roasted garlic, and hand-cut fries.
  **[2]** 🍷 **Beef Bourguignon** — Slow-braised beef in red wine with pearl onions, mushrooms, and buttery mash.
  **[3]** 🥩 **Filet Mignon** — Pan-seared tenderloin with truffle demi-glace, asparagus, and dauphinoise potatoes.
  **[4]** 🥗 **Beef Tagliata** — Sliced sirloin over wild rocket with aged parmesan and balsamic reduction.
  **[5]** 🍖 **Braised Short Ribs** — 8-hour braised short ribs with creamy polenta and citrus gremolata.

Please enter the number (1–5) or type the dish name."

---

**Fish:**

"Here are our finest Fish dishes:

  **[1]** 🐟 **Pan-Seared Salmon** — Atlantic salmon fillet with lemon-dill sauce and sautéed spinach.
  **[2]** 🐠 **Grilled Sea Bass** — Whole Mediterranean sea bass with cherry tomatoes, capers, and olive oil.
  **[3]** 🍣 **Seared Tuna Steak** — Rare-seared yellowfin tuna with wasabi crust and soy-ginger glaze.
  **[4]** 🦞 **Lobster Thermidor** — Half lobster gratinated with mustard cream and gruyère cheese.
  **[5]** 🐟 **Cod en Papillote** — Oven-baked cod fillet with fennel, citrus, and white wine in parchment.

Please enter the number (1–5) or type the dish name."

---

**Vegetarian:**

"Here are our finest Vegetarian dishes:

  **[1]** 🍄 **Wild Mushroom Risotto** — Creamy Arborio rice with porcini, shiitake, and truffle oil.
  **[2]** 🍆 **Eggplant Parmigiana** — Layered eggplant with fresh mozzarella, basil, and San Marzano tomato sauce.
  **[3]** 🫑 **Stuffed Bell Peppers** — Roasted peppers filled with quinoa, feta, and toasted pine nuts.
  **[4]** 🍝 **Spinach and Ricotta Ravioli** — Handmade pasta parcels in sage brown butter sauce.
  **[5]** 🥧 **Vegetable Wellington** — Golden puff pastry with seasonal roasted vegetables and goat cheese.

Please enter the number (1–5) or type the dish name."

---

**Vegan:**

"Here are our finest Vegan dishes:

  **[1]** 🥦 **Cauliflower Steak** — Roasted cauliflower with chimichurri, smoked paprika, and toasted almonds.
  **[2]** 🍛 **Thai Green Curry** — Fragrant coconut curry with crispy tofu, bamboo shoots, and jasmine rice.
  **[3]** 🥗 **Beetroot Carpaccio** — Thinly sliced roasted beetroot with avocado, walnut, and citrus dressing.
  **[4]** 🍄 **Stuffed Portobello Mushroom** — Grilled portobello cap with herb couscous and roasted red peppers.
  **[5]** 🍲 **Lentil Moussaka** — Layers of spiced lentils, eggplant, and potato with cashew béchamel.

Please enter the number (1–5) or type the dish name."

---

**Chef's Special:**

"Here are the Chef's Special creations:

  **[1]** 🦆 **Duck Confit** — Slow-cooked duck leg with cherry reduction and dauphinoise potatoes.
  **[2]** 🐑 **Rack of Lamb** — Herb-crusted lamb with rosemary jus and Provençal ratatouille.
  **[3]** 🍝 **Truffle Pasta** — Fresh tagliatelle with shaved black truffle, parmesan cream, and wild arugula.
  **[4]** 🦐 **Seafood Paella** — Saffron rice with king prawns, mussels, squid, and Spanish chorizo.
  **[5]** 🍔 **Wagyu Burger** — Premium wagyu patty with foie gras, caramelized onion, and toasted brioche bun.

Please enter the number (1–5) or type the dish name."

🛑 **HALT** — Wait for response.

### 3. Transition

Read fully and follow: `./step-02-confirm-selection.md`
