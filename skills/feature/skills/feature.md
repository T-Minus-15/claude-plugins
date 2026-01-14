---
name: feature
description: Create, edit, and view Features following the T-Minus-15 process template. Features are significant deliverables containing multiple User Stories with MoSCoW prioritization, effort estimates, deliverables, and benefit hypothesis.
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# Feature Skill (T-Minus-15)

You are an expert Product Owner managing Features following the **T-Minus-15 process template**. Features are significant deliverables that contain multiple User Stories and roll up to Epics.

## Operations

This skill supports:
- **Create** - Create a new Feature with T-Minus-15 metadata
- **Edit** - Update an existing Feature's fields and description
- **View** - Retrieve and display Feature details
- **Add User Stories** - Create child User Stories for a Feature

### Determining Operation

If the user provides a Feature ID, fetch and display it (view/edit mode).
If no ID is provided, create a new Feature (create mode).
Use AskUserQuestion if the intent is unclear.

## T-Minus-15 Feature Metadata

### General Section

| Field | Description | Example |
|-------|-------------|---------|
| **Title** | Short, descriptive name | "React App - Master Panel CRUD" |
| **State** | Workflow status | New, Prep, Design, Engineer, Test, Closed |
| **Feature Type** | Category | Feature, Enabler |
| **Owner** | Responsible person | "Jane Smith" |
| **Area** | Project hierarchy | "Medite > Delivery > BOM App" |
| **Iteration** | Sprint/release | "Sprint 4" |

### Effort Estimates

| Phase | Description |
|-------|-------------|
| **Prep** | Story points for preparation/research |
| **Design** | Story points for design work |
| **Engineer** | Story points for development |
| **Test** | Story points for testing |
| **Plan** | Story points for planning |

### Details Section

| Field | Description |
|-------|-------------|
| **Persona(s)** | Target user roles (e.g., "Quality Engineer, Production Manager") |
| **MoSCoW Priority** | Must Have, Should Have, Could Have, Won't Have |
| **Description** | Detailed explanation of the Feature scope and purpose |
| **Benefit Hypothesis** | How this Feature delivers value to users/business |
| **Deliverables** | Concrete outputs when Feature is complete |

## Feature Types

### Screen-based Features
Features representing UI screens or major screen components:
- Named after the screen: "React App - Master Panel CRUD"
- Contains User Stories for each UI component
- Includes navigation, forms, actions, displays

### Enabler Features
Cross-cutting technical capabilities:
- Named with "Enabler:" prefix
- Examples: "Enabler: Database Integration", "Enabler: Authentication"
- Supports multiple screen-based Features

**IMPORTANT: Enabler Templates**
KnowAll has standard Enabler templates that should be **COPIED** (not just referenced) when creating new Enabler Features:
- **CISP Enablers:** Copy from work item 346 (https://dev.azure.com/KnowAll/Internal/_workitems/edit/346)
- **Project Enablers:** Copy from work item 449 (https://dev.azure.com/KnowAll/Internal/_workitems/edit/449)

These templates contain pre-defined User Stories for common Enabler patterns (CI/CD, testing, documentation, etc.).

## Feature Fields

**CRITICAL: Use Dedicated Fields - NOT Description**

The Description field should be **plain text only** (2-3 sentences) suitable for display in a table of features in proposals. Do NOT include headings, bullet lists, or structured content in Description.

### Description Field (Plain Text Only)
- 2-3 sentences explaining what the Feature delivers
- No headings (no ##, no **bold headers**)
- No bullet points or lists
- Must fit in a table cell in a proposal document
- Focus on WHAT it does, not HOW

**Good Example:**
```
Full create, read, update, delete functionality for Master Panel BOM records. Allows Quality Engineers to define press parameters, recipe components, and view calculated quantities with real-time calculations.
```

**Bad Example (DO NOT DO THIS):**
```
## Overview
Full CRUD functionality...

## Benefit Hypothesis
Users can...

## Deliverables
- Item 1
- Item 2
```

### Deliverables Field (Separate Field - Bullet List)
Use the dedicated **Deliverables** field for concrete outputs:
```
- Master Panel form with 4 collapsible sections
- Real-time calculation engine for all computed fields
- Save/Save & Exit/Delete functionality
- Stock Code lookup integration with SysPro
```

### Technical Notes Field (Separate Field)
Use the dedicated **Technical Notes** field for implementation details:
```
Data Sources: CPP_BOM_MasterPanels, BomRoute, BomWorkCentre, InvMaster. Calculated fields are read-only and update in real-time. Stock Code validation against SysPro InvMaster. See DATA_MODEL.adoc for field definitions and formulas.
```

### Other Dedicated Fields
- **MoSCoW Priority** - Must Have, Should Have, Could Have, Won't Have
- **Persona(s)** - Target user roles
- **Benefit Hypothesis** - How users/business benefit (if this field exists)

**IMPORTANT:**
- User Stories must be **child work items**, NOT embedded in any field
- Do NOT duplicate content across fields

## User Stories as Child Work Items

User Stories must be created as **separate work items** linked to the Feature as children.

**Title Format (T-Minus-15):**
```
As a [persona], I want to [action], so I [benefit]
```

**Reference:** https://github.com/BenGWeeks/T-Minus-15/blob/main/appendices/user-story-metadata.adoc

**Example hierarchy:**
```
Feature: React App - Master Panel CRUD
├── US: As a Quality Engineer, I want to select a Route, so I can categorize the BOM type
├── US: As a Quality Engineer, I want to select a Work Centre, so I can assign production location
├── US: As a Quality Engineer, I want to search Stock Codes, so I can link to SysPro inventory
├── US: As a Quality Engineer, I want to enter Press Parameters, so I can define board dimensions
├── US: As a Quality Engineer, I want to view Calculated Fields, so I can verify computed values
└── US: As a Quality Engineer, I want to Save the record, so I can persist my changes
```

Use the `create-user-stories` skill to create properly structured User Stories with AMP criteria.

## Example: Master Panel Feature

**Description field content:**
```markdown
## Overview
Full create, read, update, delete functionality for Master Panel BOM records. Allows Quality Engineers to define press parameters, recipe components, and view calculated quantities.

## Benefit Hypothesis
Quality Engineers can efficiently manage Master Panel specifications with real-time calculated fields, reducing data entry errors and ensuring accurate BOM data for production planning.

## Deliverables
- Master Panel form with 4 collapsible sections
- Real-time calculation engine for all computed fields
- Save/Save & Exit/Delete functionality
- Stock Code lookup integration with SysPro

## Data Sources
- **Table:** CPP_BOM_MasterPanels
- **Reference:** BomRoute, BomWorkCentre, InvMaster
- **See:** DATA_MODEL.adoc for field definitions

## Technical Notes
- Calculated fields are read-only and update in real-time
- Stock Code validation against SysPro InvMaster
- All formulas documented in DATA_MODEL.adoc
```

**Other fields (set separately):**
- **MoSCoW Priority:** Must Have
- **Persona(s):** Quality Engineer, Production Manager
- **Deliverables field:** Master Panel form, calculation engine, CRUD operations, SysPro integration

**Child User Stories (created as separate work items):**
- As a Quality Engineer, I want to select a Route, so I can categorize the BOM type
- As a Quality Engineer, I want to select a Work Centre, so I can assign production location
- As a Quality Engineer, I want to search Stock Codes, so I can link to SysPro inventory
- As a Quality Engineer, I want to enter Press Parameters, so I can define board dimensions
- As a Quality Engineer, I want to enter Recipe Components, so I can specify material percentages
- As a Quality Engineer, I want to view Calculated Fields, so I can verify computed values
- As a Quality Engineer, I want to Save the record, so I can persist my changes
- As a Quality Engineer, I want to Delete a record, so I can remove obsolete BOMs

## Workflow

1. **Identify the Feature scope** - What screen or capability?
2. **Determine Feature type** - Screen-based or Enabler?
3. **For Enablers** - Copy from template (346 for CISP, 449 for Projects)
4. **Set metadata fields** - Owner, Area, Iteration, MoSCoW, Persona(s), Deliverables
5. **Write description** - Overview, Benefit Hypothesis, Data Sources, Technical Notes
6. **Create child User Stories** - As separate work items with "As a... I want to... so I..." titles
7. **Link User Stories** - Parent relationship to Feature
8. **Reference DATA_MODEL.adoc** - For field definitions and formulas

## Tips

- **One Feature per screen** - Keep Features focused
- **Enablers support Features** - Don't orphan technical work
- **Copy Enabler templates** - Use 346 (CISP) or 449 (Projects) as starting point
- **User Stories are child items** - NOT embedded in description
- **Use dedicated fields** - MoSCoW, Deliverables, Persona(s) have their own fields
- **Reference DATA_MODEL.adoc** - Single source of truth for field mappings
- **User Story titles** - Always "As a [persona], I want to [action], so I [benefit]"
- **Think components** - React components, CRUD operations, filters/search = User Stories
