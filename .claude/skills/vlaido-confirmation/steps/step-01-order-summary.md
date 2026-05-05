# Step 1: Order Summary

Present formatted order summary and ask for yes/no confirmation.

## Instructions

### 1. Load Order State

Read all `order_state` fields from `{outputFile}`. `category` and `main_course` must NOT be null.

### 2. Present Summary

"📋 **Here is your complete order summary:**

┌──────────────────────────────────────────────────┐
│                                                  │
│  🏷️  **Category:**    {category}                  │
│                                                  │
│  🍽️  **Main Course:** {main_course}               │
│      _{main_course_description}_                  │
│                                                  │
│  🍰 **Dessert:**      {dessert or 'No dessert'}   │
│      _{description if selected}_                  │
│                                                  │
│  🥤 **Drink:**        {drink or 'No drink'}       │
│                                                  │
└──────────────────────────────────────────────────┘

Does everything look correct?

Reply **yes** to confirm, or **no** to make changes."

🛑 **HALT** — Wait for response.

### 3. Transition

Read fully and follow: `./step-02-final-confirmation.md`
