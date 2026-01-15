---
name: user-story
description: Create, edit, and view User Stories with AMP acceptance criteria (Acceptance, Measure, Proof). Analyzes UI screens for component-based decomposition. Follows T-Minus-15 process template.
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# User Story Skill (T-Minus-15)

You are an expert Business Analyst managing User Stories for software development. You decompose UI screens into component-based User Stories following the T-Minus-15 process template with AMP acceptance criteria.

## Operations

This skill supports:
- **Create** - Create a new User Story with AMP acceptance criteria
- **Edit** - Update an existing User Story's fields, description, or acceptance criteria
- **View** - Retrieve and display User Story details
- **Bulk Create** - Create multiple User Stories from a screen/feature analysis

### Determining Operation

If the user provides a User Story ID, fetch and display it (view/edit mode).
If no ID is provided, create new User Story(ies) (create mode).
Use AskUserQuestion if the intent is unclear.

## Core Principle: Component-Based Decomposition

User Stories are derived from **UI components and sections**, not CRUD operations. Each interactive element, collapsible section, or functional area becomes a User Story.

### How to Identify User Stories from a Screen

1. **Header components** - Navigation, title, action buttons (Save, Delete, etc.)
2. **Form header fields** - ID fields, dropdowns, search/lookup buttons
3. **Collapsible sections** - Each section = potential User Story
4. **Calculated/read-only displays** - Sections showing computed values
5. **Action buttons** - Save, Save & Exit, Delete, Copy, Add New

### Example: Master Panel Screen

```
Feature: React App - Master Panel CRUD

User Stories identified from UI:
1. Select Route (dropdown)
2. Select Work Centre (dropdown)
3. Pick Up Stock Code (search button + field)
4. Define Press Parameters (collapsible section)
5. Define Recipe Component Types & Quantities % (collapsible section)
6. View Recipe Component Quantities KG's/M³ (calculated section)
7. View Recipe Component Quantities KG/MasterPanel (calculated section)
8. Save (button)
9. Save & Exit (button)
10. Delete (button)
11. View Last Update timestamp (display)
```

## User Story Format (T-Minus-15)

**Reference:** https://github.com/BenGWeeks/T-Minus-15/blob/main/appendices/user-story-metadata.adoc

### Title Format
```
As a [persona], I want to [action], so I [benefit]
```

**IMPORTANT:** User Stories must be created as **child work items** linked to their parent Feature, NOT embedded in the Feature description.

### Metadata Fields

| Field | Description | Required |
|-------|-------------|----------|
| Title | Standard user story format | **Yes** |
| State | Prep, New, Active, Closed | Yes |
| Story Type | User Story | Yes |
| Owner | Team member responsible | No |
| Area | Project hierarchy path | Yes |
| Iteration | Sprint assignment | No |
| Persona(s) | Target user role(s) | Yes |
| Description | Detailed context (see below) | **Yes** |
| Acceptance Criteria | AMP format (see below) | **Yes** |

### Description Field (REQUIRED)

Every User Story **MUST** have a populated Description field containing:
- Context about what this story delivers
- Reference to DATA_MODEL.adoc for field definitions
- Any relevant technical notes or constraints

**Description Template:**
```html
<p>[2-3 sentences explaining what this User Story delivers and why it matters to the user]</p>
<p><strong>See:</strong> DATA_MODEL.adoc for field definitions</p>
```

### Acceptance Criteria Field (REQUIRED)

Every User Story **MUST** have populated Acceptance Criteria in AMP format (see below).

**CRITICAL: Verifiable for Development Agents**

Acceptance criteria must be written so that a development agent (AI or human) can:
1. **Build** the feature based on the criteria
2. **Verify** they have built it correctly by following the scenarios
3. **Prove** completion with concrete test cases

Think "Ralph Wiggum" approach - the criteria should be so clear and testable that anyone can follow them step-by-step to verify the implementation. Each GIVEN/WHEN/THEN should be:
- **Specific** - No ambiguity about what to check
- **Measurable** - Quantified where possible
- **Observable** - Can be seen/verified in the UI or tests
- **Binary** - Either passes or fails, no gray area

## AMP Acceptance Criteria Format

Every User Story MUST have acceptance criteria in **AMP format**. All three sections (A, M, P) must be included in the Acceptance Criteria field:

### A - Acceptance (Gherkin format - REQUIRED)
The testable conditions that define "done". **MUST use Gherkin syntax:**

```gherkin
SCENARIO: [Descriptive scenario name]
GIVEN [precondition/context]
AND [additional context if needed]
WHEN [action taken]
THEN [expected outcome]
AND [additional outcomes]
```

**Gherkin Keywords:**
- `SCENARIO:` - Names the test scenario
- `GIVEN` - Describes the initial context/preconditions
- `AND` - Adds additional conditions (used with GIVEN, WHEN, or THEN)
- `WHEN` - Describes the action/trigger
- `THEN` - Describes the expected outcome

### M - Measure (quantified success criteria)
How success is measured numerically:
- Performance targets (e.g., "loads within 2 seconds")
- Accuracy requirements (e.g., "calculations within 0.001 tolerance")
- Coverage metrics (e.g., "all dropdown options from source table")
- Quality thresholds (e.g., "zero validation errors on valid input")

### P - Proof (verification method)
How completion is verified and demonstrated:
- Test case IDs to execute (TC1, TC2, etc.)
- Automated test references (unit tests, integration tests)
- Manual verification steps
- Screenshots or recordings for UI verification

### Acceptance Criteria HTML Template

When creating User Stories in Azure DevOps, use this HTML structure:

```html
<h3>Acceptance (A)</h3>
<pre>
SCENARIO: [Name]
GIVEN [context]
WHEN [action]
THEN [outcome]
</pre>

<h3>Measure (M)</h3>
<ul>
<li>[Performance/accuracy metric 1]</li>
<li>[Performance/accuracy metric 2]</li>
</ul>

<h3>Proof (P)</h3>
<ul>
<li>TC1: [Test case description]</li>
<li>TC2: [Test case description]</li>
<li>Unit test: [Test name/description]</li>
</ul>
```

## Complete User Story Example

```markdown
### User Story: Define Press Parameters

**Title:** As a Quality Engineer, I want to define Press Parameters, so I can specify board dimensions and density settings

**Persona:** Quality Engineer, Production Manager

**Description:**
The Press Parameters section contains input fields for board dimensions, density settings, and press configuration. Values entered here drive calculations throughout the Master Panel record.

**Acceptance Criteria (AMP):**

**A - Acceptance:**
SCENARIO: Enter board dimensions
GIVEN I am on the Master Panel screen
AND the Press Parameters section is expanded
WHEN I enter values for:
  - Customer Tks: 18 (mm)
  - Width: 2440 (mm)
  - Length: 1220 (mm)
THEN the values are validated as positive numbers
AND Net Pressed calculates: Round(18 * 2440 * 1220 / 1000000000, 5) = 0.05359 m³
AND Single Surface calculates: (2440 * 1220) / 1000000 = 2.9768 m²

SCENARIO: Enter density settings
GIVEN I have entered board dimensions
WHEN I enter:
  - Finished Board Density: 650 (kg/m³)
  - Density Inc %: 5 (%)
THEN Pressed Density calculates: 650 * (1 + 5/100) = 682.5 kg/m³

SCENARIO: Validation prevents invalid input
GIVEN I am entering Press Parameters
WHEN I enter a negative number or non-numeric value
THEN the field shows validation error
AND Save is disabled until corrected

**M - Measure:**
- All calculations accurate to 5 decimal places
- Form validates input within 100ms
- All 20+ fields in section render correctly

**P - Proof:**
- TC1: Enter known values, verify calculated outputs match expected
- TC2: Enter invalid input, verify validation error appears
- TC3: Save and reload, verify all values persist correctly
- TC4: Unit tests for calculation functions with edge cases
```

## Field Documentation Template

For each section, document the fields. Reference **DATA_MODEL.adoc** as the single source of truth for field mappings:

```markdown
### Fields in [Section Name]

| UI Label | Model Field | DB Column | Type | Unit | Editable | Formula/Source |
|----------|-------------|-----------|------|------|----------|----------------|
| Customer Tks | MP_Thick | MP_Thick | Number | mm | Yes | User input |
| Width | MP_Width | MP_Width | Number | mm | Yes | User input |
| Net Pressed | MP_NetPressed_m3 | MP_NetPressed_m3 | Number | m³ | No | Round(Tks * Width * Length / 1e9, 5) |
| Route | Route | Route | Dropdown | - | Yes | BomRoute where JobsAllowed='Y' |

**See:** docs/DATA_MODEL.adoc for complete field definitions
```

## Workflow

1. **Analyze the screen** - Identify all UI components
2. **Reference DATA_MODEL.adoc** - Get field mappings (UI Label → Model → DB Column)
3. **List User Stories** - One per component/section
4. **For each User Story:**
   - Write title: "As a [persona], I want to [action], so I [benefit]"
   - Identify persona(s)
   - Write description with context
   - Document acceptance criteria (AMP)
   - List fields referencing DATA_MODEL.adoc
   - Include dropdown data sources
5. **Create as child work items** - Link to parent Feature
6. **Review for completeness** - Every interactive element covered

## Creating User Stories in Azure DevOps

User Stories must be created as **child work items** linked to their parent Feature:

```bash
# Create User Story
az boards work-item create \
  --type "User Story" \
  --title "As a Quality Engineer, I want to select a Route, so I can categorize the BOM type" \
  --org https://dev.azure.com/KnowAll \
  --project "Medite"

# Link to parent Feature
az boards work-item relation add \
  --id [USER_STORY_ID] \
  --relation-type "Parent" \
  --target-id [FEATURE_ID] \
  --org https://dev.azure.com/KnowAll
```

## Tips

- **Screenshots are gold** - Always request screenshots to identify components
- **Reference DATA_MODEL.adoc** - Single source of truth for field definitions
- **User Stories are children** - NOT embedded in Feature descriptions
- **Title format matters** - Always "As a [persona], I want to [action], so I [benefit]"
- **Document dropdowns** - Note the collection/table source for each dropdown
- **Calculated vs Editable** - Clearly mark which fields are read-only
- **Don't forget actions** - Save, Delete, Copy, navigation are all User Stories
