---
outputFile: "vlaido_order_log.md
---

# Step 1: Customer Greeting

Collect name and preferred language, prepare the order log. Never auto-detect or pre-fill — always ask.

## Instructions

### 1. Prepare Output File

> All file operations are invisible to the customer.

Check if `{outputFile}` exists:
- **Exists with `status: confirmed`**: Reset with fresh template (instruction 2)
- **Exists with `status: in-progress`, `customer_name: null`**: Reset with fresh template
- **Exists with `status: in-progress`, `customer_name` set**: Execute **Continuation Routing** below
- **Does not exist**: Create with template (instruction 2)

#### Continuation Routing

Check `order_state` fields and route to the furthest incomplete step:

| Condition | Route to |
|---|---|
| `drink` is set | `../../vlaido-confirmation/steps/step-01-order-summary.md` |
| `dessert` is set | `../../vlaido-drinks/steps/step-01-present-options.md` |
| `main_course` is set | `../../vlaido-dessert/steps/step-01-present-options.md` |
| `category` is set | `../../vlaido-main-course/steps/step-01-present-options.md` |
| `category` is null | Continue to instruction 3 |

Before routing, greet: "Welcome back, **{customer_name}**! Let me pick up where we left off."
Briefly list existing selections (show "skipped" for `None` values). Then route.

### 2. Output File Template

Write this content to `{outputFile}`:

```yaml
---
stepsCompleted: []
order_state:
  customer_name: null
  anonymous: false
  language: null
  category: null
  main_course: null
  main_course_description: null
  dessert: null
  dessert_description: null
  drink: null
  order_reference: null
  status: in-progress
---
```

Followed by:

```markdown
# 🍽️ Vlaido Bistro — Order Log

> Progressively built as the ordering workflow executes.

---
```

### 3. Welcome and Ask for Name

Display:

"🍽️ **Welcome to Vlaido Bistro!**

We are delighted to have you here today. Before we begin, may I have your name, please?"

🛑 **HALT** — Wait for response.

### 4. Ask for Preferred Language

**If name provided:**
"Wonderful to meet you, **{name}**!"

**If customer declines to share name (anonymous):**

"Wonderful to have you as our valued guest!"

Then ask:

"What language would you like me to communicate in? (e.g., English, French, Arabic, Spanish…)"

🛑 **HALT** — Wait for response.

### 5. Confirm and Transition

Acknowledge in the chosen language from this point forward:

"Perfect! I'll communicate in **{language}** from now on. Allow me to guide you through our menu so we can prepare the perfect meal for you.

Let's begin by choosing your preferred dining category."

### 6. Update Output File

- Set `order_state.customer_name` (or "Guest" if anonymous)
- Set `order_state.anonymous` to `true` if no name given
- Set `order_state.language` to chosen language 
- Add `step-01-greeting` to `stepsCompleted`

Append:

```markdown

## 🎉 Welcome

**Date:** {current date and time, Paris timezone}
**Customer:** {customer_name}
**Language:** {language}

---
```

### 7. Next Step

Read fully and follow: `./step-02-category-selection.md`
