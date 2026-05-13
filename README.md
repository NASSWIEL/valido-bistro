<div align="center">

# 🍽️ Vlaido Bistro

**A conversational restaurant ordering system built with Claude Code skills**

[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skills-blueviolet?style=flat-square&logo=anthropic)](https://claude.ai/code)
[![BMAD](https://img.shields.io/badge/Architecture-BMAD-orange?style=flat-square)](https://github.com/bmad-framework)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)]()

<br/>

*Demonstrates how to build multi-step, state-managed, human-interactive workflows<br/>using Claude Code's native skill architecture — no external dependencies.*

</div>

---

## What is Vlaido Bistro?

Vlaido Bistro is a fully interactive dining experience that lives inside your Claude Code session. It guides customers through a complete restaurant order — from greeting and dietary preference to dessert and final confirmation — using a chain of **5 interconnected skills** with strict input validation and session-persistent state.

It was built as a practical reference for the **BMAD (modular workflow) pattern** in Claude Code: how to decompose a complex, multi-turn interaction into discrete, resumable steps that hand off state cleanly.

```
User: "I am ready to order."

🍽️  Welcome to Vlaido Bistro!
     What's your name?

> Naif

     Great to have you, Naif. Please choose your dietary preference:

     1. 🥩  Beef
     2. 🐟  Fish
     3. 🥗  Vegetarian
     4. 🌱  Vegan
     5. 👨‍🍳  Chef's Special

> 5

     Excellent choice. Here are tonight's Chef's Special main courses...
```

---

## Features

| | Feature | Description |
|---|---|---|
| 🔗 | **Chained skills** | 5 skills execute in sequence, each triggered by the previous |
| ⏸️ | **Halt-and-wait** | Every step pauses for validated user input — nothing is assumed |
| 🔄 | **Session resume** | Mid-order interruptions resume at the correct step on re-invoke |
| ✅ | **Strict validation** | Case-insensitive, number or name input, with re-prompt on ambiguity |
| 🌱 | **Diet-aware menus** | Main courses and desserts adapt to the selected dietary category |
| 📋 | **Order log** | Appends a structured markdown receipt with reference number |
| 🔢 | **Reference numbers** | Auto-generated `ORD-YYYY-XXXX` for every confirmed order |
| 📦 | **Zero dependencies** | Pure Markdown + YAML — no packages, no setup, no config |

---

## Architecture

The system is composed of 5 skills, each owning 2 steps. Skills chain automatically — no routing logic needed in the host session.

```
vlaido-welcome
  ├── step-01: greeting + name collection
  └── step-02: dietary category selection (Beef · Fish · Vegetarian · Vegan · Chef's Special)
        │
        ▼
vlaido-main-course
  ├── step-01: present 5 category-specific dishes
  └── step-02: confirm selection
        │
        ▼
vlaido-dessert
  ├── step-01: present desserts (standard or vegan variant)
  └── step-02: confirm selection
        │
        ▼
vlaido-drinks
  ├── step-01: present drink options
  └── step-02: confirm selection
        │
        ▼
vlaido-confirmation
  ├── step-01: full order summary
  └── step-02: confirm → write order log  |  restart → back to welcome
```

**State** flows through `vlaido-order-log.md` (YAML frontmatter). Each completed step appends its output and marks itself done, enabling accurate resume detection on re-invocation.

```
.claude/skills/
├── vlaido-welcome/
│   ├── SKILL.md
│   ├── workflow.md
│   └── steps/
│       ├── step-01-greeting.md
│       └── step-02-category-selection.md
├── vlaido-main-course/   (same structure)
├── vlaido-dessert/       (same structure)
├── vlaido-drinks/        (same structure)
└── vlaido-confirmation/  (same structure)
```

---

## Menu

<details>
<summary><b>🥩 Beef</b></summary>

| # | Dish |
|---|------|
| 1 | Grilled Ribeye Steak |
| 2 | Beef Bourguignon |
| 3 | Filet Mignon |
| 4 | Beef Tagliata |
| 5 | Braised Short Ribs |

</details>

<details>
<summary><b>🐟 Fish</b></summary>

| # | Dish |
|---|------|
| 1 | Pan-Seared Salmon |
| 2 | Grilled Sea Bass |
| 3 | Seared Tuna Steak |
| 4 | Lobster Thermidor |
| 5 | Cod en Papillote |

</details>

<details>
<summary><b>🥗 Vegetarian</b></summary>

| # | Dish |
|---|------|
| 1 | Wild Mushroom Risotto |
| 2 | Eggplant Parmigiana |
| 3 | Stuffed Bell Peppers |
| 4 | Spinach and Ricotta Ravioli |
| 5 | Vegetable Wellington |

</details>

<details>
<summary><b>🌱 Vegan</b></summary>

| # | Dish |
|---|------|
| 1 | Cauliflower Steak |
| 2 | Thai Green Curry |
| 3 | Beetroot Carpaccio |
| 4 | Stuffed Portobello Mushroom |
| 5 | Lentil Moussaka |

</details>

<details>
<summary><b>👨‍🍳 Chef's Special</b></summary>

| # | Dish |
|---|------|
| 1 | Duck Confit |
| 2 | Rack of Lamb |
| 3 | Truffle Pasta |
| 4 | Seafood Paella |
| 5 | Wagyu Burger |

</details>

<details>
<summary><b>🍮 Desserts</b></summary>

**Standard** — Tiramisu · Crème Brûlée · Chocolate Fondant · Panna Cotta · Tarte Tatin

**Vegan** — Dark Chocolate Mousse · Coconut Panna Cotta · Mango Sorbet Trio · Apple Crumble · Avocado Lime Cheesecake

</details>

<details>
<summary><b>🥤 Drinks</b></summary>

Still Water · Sparkling Water · Fresh Orange Juice · House Red Wine · Mint Tea

</details>

---

## Getting Started

**Requirements:** [Claude Code](https://claude.ai/code) — nothing else.

Clone or copy this repository into any directory you open with Claude Code. The `.claude/skills/` folder is picked up automatically.

```bash
git clone https://github.com/YOUR_USERNAME/vlaido-bistro
cd vlaido-bistro
claude  # open with Claude Code
```

Then, in your Claude Code session, say anything that signals ordering intent:

```
I am ready to order.
I'd like to place an order.
Let me order something.
```

The `vlaido-welcome` skill activates and the experience begins.

---

## How BMAD Skills Work

Each skill follows a three-layer structure:

```
SKILL.md        → entry point, description, activation trigger
workflow.md     → goal, role, and step delegation instructions
steps/
  step-XX.md   → mandatory rules, execution protocol, task goal, instruction sequence
```

Skills communicate through a shared state file (`vlaido-order-log.md`) whose YAML frontmatter is read and written at each step. This makes the workflow:

- **Resumable** — re-invoking mid-order picks up exactly where it left off
- **Auditable** — every transition is written to the log before proceeding
- **Decoupled** — skills don't import each other; state is the contract

---

## Extending the System

To add a new course or modify the menu, edit the corresponding `step-01-present-options.md` file inside the skill's `steps/` folder. The validation and routing logic in `step-02` handles any list of options automatically.

To add an entirely new step to the flow:

1. Create a new skill folder under `.claude/skills/`
2. Add `SKILL.md`, `workflow.md`, and your step files
3. Update the previous skill's final step to hand off to the new one
4. Add the new state fields to the order log frontmatter schema

---

## Contributing

This is a reference implementation. Issues and PRs are welcome — especially:

- New dietary categories or menu variants
- Localization (French, Arabic, etc.)
- A web-based order log viewer
- Integration with actual POS or reservation systems

---

<div align="center">

Built with [Claude Code](https://claude.ai/code) · Powered by the BMAD skill pattern

</div>
