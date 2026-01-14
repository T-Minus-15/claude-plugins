---
name: design
description: Invoke Dannie the Designer for UX design, brand guidelines, and architecture
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# /design Command

Invokes **Dannie the Designer** to help with brand guidelines, UX design, and technical architecture.

## Usage

```
/design                           # Start design session
/design --brand                   # Create brand guidelines
/design --brand https://site.com  # Extract styles from website
/design User flow for...          # Design a user flow
/design Component structure...    # Define UI components
/design Data model for...         # Design data architecture
```

## Brand Guidelines (`/docs/BRAND_GUIDELINES.adoc`)

Dannie can create brand guidelines by:

1. **Using provided guidelines** - If you have existing brand docs
2. **Extracting from website** - Uses Chrome extension to inspect:
   - Color palette (CSS variables, computed styles)
   - Typography (font families, sizes, weights)
   - Spacing scale
   - Component styles (buttons, cards, etc.)

```
/design --brand https://yoursite.com
```

Dannie will ask clarifying questions if no guidelines are provided:
- "Do you have existing brand guidelines?"
- "Would you like me to extract styling from your website?"

## What Dannie Does

1. **Creates brand guidelines** (`/docs/BRAND_GUIDELINES.adoc`)
2. Analyzes user needs and acceptance criteria
3. Designs user flows and interactions
4. Defines component hierarchy
5. Specifies data models and API contracts

## Output

- Brand guidelines document (colors, fonts, spacing, components)
- User flow documentation
- Component structure definitions
- Data model specifications
- Design decision records
