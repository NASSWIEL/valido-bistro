# Vlaido Bistro Ordering System

A BMAD-inspired human-interactive restaurant ordering workflow built on Claude Code skill architecture. This project demonstrates a complete dining experience at **Vlaido Bistro**, guiding customers through dietary category selection, main course, dessert, drink choices, and final order confirmation.

## Overview

Vlaido is a minimal, self-contained ordering module that simulates a restaurant experience. It follows BMAD framework principles with step-by-step human interaction, state tracking, input validation, and conditional flow progression. The system uses Claude Code skills to manage the workflow, ensuring a seamless and validated ordering process.

The primary objective of this project is to understand how workflows function with Claude Code skills, showcasing the integration of multiple skills in a sequential, state-managed process.

## Features

- **Interactive Ordering Workflow**: Step-by-step guidance through the entire ordering process
- **Dietary Category Selection**: Choose from Beef, Fish, Vegetarian, Vegan, or Chef's Special
- **Personalized Menus**: Category-specific main courses and desserts
- **Input Validation**: Strict validation with polite re-prompts for invalid inputs
- **State Persistence**: Order state tracked across sessions in a markdown log file
- **Order Confirmation**: Full order review with reference number generation

## Menu Options

### Dietary Categories
1. 🥩 Beef
2. 🐟 Fish
3. 🥗 Vegetarian
4. 🌱 Vegan
5. 👨‍🍳 Chef's Special

### Sample Main Courses
- **Beef**: Grilled Ribeye Steak, Beef Bourguignon, Filet Mignon, etc.
- **Fish**: Pan-Seared Salmon, Grilled Sea Bass, Seared Tuna Steak, etc.
- **Vegetarian**: Wild Mushroom Risotto, Eggplant Parmigiana, Stuffed Bell Peppers, etc.
- **Vegan**: Cauliflower Steak, Thai Green Curry, Beetroot Carpaccio, etc.
- **Chef's Special**: Duck Confit, Rack of Lamb, Truffle Pasta, etc.

### Desserts
- Standard: Tiramisu, Crème Brûlée, Chocolate Fondant, Panna Cotta, Tarte Tatin
- Vegan: Dark Chocolate Mousse, Coconut Panna Cotta, Mango Sorbet Trio, etc.

### Drinks
- Still Water, Sparkling Water, Fresh Orange Juice, House Red Wine, Mint Tea

## Installation & Setup

This project is designed to run within a Claude Code environment. No external dependencies or configuration files are required.

1. Ensure you have Claude Code set up in your workspace.
2. The skills are located in the `.claude/skills/` directory.
3. The system is fully self-contained and ready to use.

## Usage

To start the ordering process, simply express your intent to order in natural language:

- "I am ready to order."
- "I'd like to order something."
- "I want to place an order."

The `vlaido-welcome` skill will activate and guide you through:
1. Greeting and customer name collection
2. Dietary category selection
3. Main course selection (based on category)
4. Dessert selection
5. Drink selection
6. Final order confirmation

The system will create and maintain an order log file (`vlaido-order-log.md`) in the project root, tracking your progress and final order.

## Architecture

The system consists of 5 interconnected skills:

- `vlaido-welcome`: Entry point for greeting and category selection
- `vlaido-main-course`: Presents category-specific main course options
- `vlaido-dessert`: Offers dessert choices (vegan-aware)
- `vlaido-drinks`: Provides drink selection
- `vlaido-confirmation`: Summarizes and confirms the complete order

Each skill follows BMAD conventions with YAML frontmatter, workflow delegation, and step-by-step execution protocols.

## State Management

Order state is persisted in the frontmatter of the output file, allowing seamless continuation across sessions. The system tracks:
- Customer name
- Selected category
- Main course and description
- Dessert and description
- Drink choice
- Order reference number
- Completion status

## Validation Rules

- Strict input matching with case-insensitive validation
- Polite re-prompting for invalid inputs
- No silent assumptions or defaults
- Ambiguity resolution through clarification requests

## Output

The workflow generates a comprehensive order log in markdown format, including:
- Welcome section with date and customer details
- Category selection confirmation
- Detailed menu item descriptions
- Final order summary with reference number
- Timestamped completion

## Contributing

This is a demonstration project showcasing BMAD framework implementation. For modifications or extensions, ensure adherence to the established skill architecture and validation protocols.
