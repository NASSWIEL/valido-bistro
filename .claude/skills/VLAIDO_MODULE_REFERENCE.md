# Vlaido Bistro — Module Reference Guide

> **Module:** vlaido
> **Version:** 1.0.0
> **Type:** BMAD-inspired human-interactive ordering workflow
> **Platform:** Claude Code skill architecture
> **Location:** `.claude/skills/vlaido-*`

---

## Overview

**Vlaido** is a minimal, self-contained, human-interactive restaurant ordering module built on BMAD framework conventions. It simulates a complete dining experience at **Vlaido Bistro**, guiding the customer (user) through category selection, main course, dessert, drink, and final order confirmation — one step at a time.

The module demonstrates BMAD's core principles:

| Principle | How Vlaido Implements It |
|---|---|
| **Skill activation triggers** | `vlaido-welcome` activates on natural-language ordering intent |
| **Step-by-step human interaction** | Each step halts and waits for validated user input |
| **State tracking** | `order_state` in output file frontmatter persists across skills |
| **Input validation** | Strict matching rules with polite re-prompts on invalid input |
| **Conditional flow progression** | Category-dependent menus, confirmation/rejection branching |
| **Append-only document building** | Order log progressively built as each skill executes |

---

## Module Architecture

```
.claude/skills/
├── vlaido-welcome/
│   ├── SKILL.md                          ← Entry point (user trigger)
│   ├── workflow.md                       ← Config loading + delegation
│   └── steps/
│       ├── step-01-greeting.md           ← Welcome + order log creation
│       └── step-02-category-selection.md ← 5 dietary categories
│
├── vlaido-main-course/
│   ├── SKILL.md
│   ├── workflow.md
│   └── steps/
│       ├── step-01-present-options.md    ← Category-specific dishes
│       └── step-02-confirm-selection.md  ← Validate dish choice
│
├── vlaido-dessert/
│   ├── SKILL.md
│   ├── workflow.md
│   └── steps/
│       ├── step-01-present-options.md    ← 5 dessert options
│       └── step-02-confirm-selection.md  ← Validate dessert choice
│
├── vlaido-drinks/
│   ├── SKILL.md
│   ├── workflow.md
│   └── steps/
│       ├── step-01-present-options.md    ← 5 drink options
│       └── step-02-confirm-selection.md  ← Validate drink choice
│
└── vlaido-confirmation/
    ├── SKILL.md
    ├── workflow.md
    └── steps/
        ├── step-01-order-summary.md      ← Full order review
        └── step-02-final-confirmation.md ← Confirm or restart
```

**Total:** 5 skills, 5 workflows, 10 step files = **20 files**

---

## Workflow Flow

```
User says: "I'd like to order" / "I am ready to order"
        │
        ▼
┌─────────────────────────────┐
│   vlaido-welcome            │
│   step-01: Greeting         │ ← Creates order log, greets customer
│   step-02: Category Select  │ ← [1] Beef [2] Fish [3] Vegetarian
│             ▼               │   [4] Vegan [5] Chef's Special
│         HALT & WAIT         │
│         VALIDATE            │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│   vlaido-main-course        │
│   step-01: Present Options  │ ← 5 dishes per category
│   step-02: Confirm Select   │
│         HALT & WAIT         │
│         VALIDATE            │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│   vlaido-dessert            │
│   step-01: Present Options  │ ← Category-aware (vegan/standard)
│   step-02: Confirm Select   │
│         HALT & WAIT         │
│         VALIDATE            │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│   vlaido-drinks             │
│   step-01: Present Options  │ ← Water, Juice, Wine, Tea
│   step-02: Confirm Select   │
│         HALT & WAIT         │
│         VALIDATE            │
└─────────────┬───────────────┘
              │
              ▼
┌─────────────────────────────┐
│   vlaido-confirmation       │
│   step-01: Order Summary    │ ← Full review of all selections
│   step-02: Final Confirm    │
│         HALT & WAIT         │
│         ┌───┴───┐           │
│        YES      NO          │
│         │        │           │
│    ORD-XXXX  RESTART        │
│    (END)     ↗ category     │
└─────────────────────────────┘
```

---

## Configuration

Vlaido is fully self-contained — no external configuration files needed. All settings are embedded in the skill files:

| Setting | Value | Where |
|---|---|---|
| Output file | `vlaido-order-log.md` in project root | workflow.md frontmatter |
| Language | English (hardcoded) | All step files |
| Customer name | Asked during greeting | step-01-greeting.md |

**Output file:** `{project-root}/vlaido-order-log.md`

**CRITICAL:** This module does NOT use `_bmad/`, `config.yaml`, or any external configuration. All file operations are silent and invisible to the customer.

---

## State Management

All state is persisted in the output file frontmatter:

```yaml
---
stepsCompleted:
  - step-01-greeting
  - step-02-category-selection
  - main-course-step-02-confirm-selection
  - dessert-step-02-confirm-selection
  - drinks-step-02-confirm-selection
  - confirmation-step-02-final-confirmation
order_state:
  customer_name: "Naif"          # Asked during greeting
  category: "Beef"              # Set by vlaido-welcome
  main_course: "Filet Mignon"   # Set by vlaido-main-course
  main_course_description: "..."
  dessert: "Tiramisu"           # Set by vlaido-dessert
  dessert_description: "..."
  drink: "House Red Wine"       # Set by vlaido-drinks
  order_reference: "ORD-2026-4217"  # Set by vlaido-confirmation
  status: "confirmed"           # in-progress → confirmed
---
```

> **Note:** Each step's `stepsCompleted` entry is prefixed with its skill name to avoid naming collisions across skills (e.g., `drinks-step-02-confirm-selection` instead of just `step-02-confirm-selection`). Welcome steps are unprefixed as they are unique.

### Continuation Routing

If the user re-invokes the ordering workflow mid-order, `step-01-greeting.md` checks `order_state` fields top-down to resume at the correct point:

| Condition | Routes To |
|---|---|
| `order_state.drink` is set | vlaido-confirmation |
| `order_state.dessert` is set | vlaido-drinks |
| `order_state.main_course` is set | vlaido-dessert |
| `order_state.category` is set | vlaido-main-course |
| Nothing set | step-02-category-selection |

---

## Validation Rules

Every step that collects user input enforces these rules:

### 1. Halt-and-Wait Protocol
Every step presenting options halts execution completely. The agent never assumes, skips, or pre-fills answers.

### 2. Strict Input Matching
- **Numbers:** Exact match (1–5)
- **Names:** Case-insensitive match on full name or predefined aliases
- **Partial:** Unambiguous partial matches accepted (e.g., "bee" → Beef)
- **Rejected:** Blank input, vague phrases, nonsensical text

### 3. Re-prompt Loop
On invalid input:
1. Display polite error message
2. Re-present the same options unchanged
3. Halt and wait again
4. Repeat until valid

### 4. Echo-back Confirmation
Every valid selection is echoed back to the customer before proceeding.

### 5. No Silent Progression
Ambiguous input is never silently interpreted. When in doubt, the agent re-prompts.

### 6. Ambiguity Resolution
When input could match multiple options (e.g., "water" → Still or Sparkling), the agent asks for clarification instead of defaulting.

---

## Menu Reference

### Dietary Categories
| # | Category | Icon |
|---|---|---|
| 1 | Beef | 🥩 |
| 2 | Fish | 🐟 |
| 3 | Vegetarian | 🥗 |
| 4 | Vegan | 🌱 |
| 5 | Chef's Special | 👨‍🍳 |

### Main Courses (per category)

**Beef:** Grilled Ribeye Steak, Beef Bourguignon, Filet Mignon, Beef Tagliata, Braised Short Ribs

**Fish:** Pan-Seared Salmon, Grilled Sea Bass, Seared Tuna Steak, Lobster Thermidor, Cod en Papillote

**Vegetarian:** Wild Mushroom Risotto, Eggplant Parmigiana, Stuffed Bell Peppers, Spinach and Ricotta Ravioli, Vegetable Wellington

**Vegan:** Cauliflower Steak, Thai Green Curry, Beetroot Carpaccio, Stuffed Portobello Mushroom, Lentil Moussaka

**Chef's Special:** Duck Confit, Rack of Lamb, Truffle Pasta, Seafood Paella, Wagyu Burger

### Desserts

**Standard** (Beef, Fish, Vegetarian, Chef's Special): Tiramisu, Crème Brûlée, Chocolate Fondant, Panna Cotta, Tarte Tatin

**Vegan**: Dark Chocolate Mousse, Coconut Panna Cotta, Mango Sorbet Trio, Apple Crumble, Avocado Lime Cheesecake

### Drinks
Still Water, Sparkling Water, Fresh Orange Juice, House Red Wine, Mint Tea

---

## BMAD Conventions Applied

| Convention | Implementation |
|---|---|
| **SKILL.md format** | YAML frontmatter (`name`, `description`) + delegation to `./workflow.md` |
| **workflow.md structure** | Goal → Role → Workflow Architecture → Activation (self-contained) → Execution (delegate to step) |
| **Step file structure** | MANDATORY EXECUTION RULES → EXECUTION PROTOCOLS → CONTEXT BOUNDARIES → YOUR TASK/STEP GOAL → Sequence of Instructions → CRITICAL STEP COMPLETION NOTE → SYSTEM SUCCESS/FAILURE METRICS |
| **State tracking** | `stepsCompleted` array + `order_state` object in output file frontmatter |
| **Step processing** | Read completely → Follow sequence → Wait for input → Validate → Save state → Load next |
| **Critical rules** | 🛑 Never load multiple steps, 📖 Always read full step, ⏸️ Always halt at menus, 🚫 Never skip validation, 🔇 Always write files silently |
| **Transition pattern** | Direct step-to-step: `../../vlaido-X/steps/step-01-*.md` (bypasses SKILL.md + workflow.md for speed) |
| **Config loading** | Self-contained — no external config. Language=English, name asked at greeting, output file in project root |
| **Document building** | Append-only to output file with frontmatter updates (all silent) |
| **Communication** | English, second-person imperative voice |

---

## How to Run

In a Claude Code session, simply type any ordering intent:

- "I am ready to order."
- "I'd like to order something."
- "I want to place an order."

The `vlaido-welcome` skill will activate and guide you through the entire ordering experience.

---

## Order Log Output

The workflow produces a progressively-built markdown file at `{output_folder}/vlaido-order-log.md` with the following sections:

1. **Welcome** — Date, customer name, greeting
2. **Category Selection** — Chosen dietary category
3. **Main Course** — Selected dish with description
4. **Dessert** — Selected dessert with description
5. **Drink** — Selected beverage
6. **Order Confirmation** — Reference number, final order table, timestamp

Each section is appended as the corresponding skill completes, matching BMAD's append-only document building pattern.
