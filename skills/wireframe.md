---
name: wireframe
description: Create and maintain ASCII wireframes for UI screens. Provides engineers with visual layout specifications without requiring design tools.
allowed-tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion
---

# Wireframe Skill

Create and maintain `/docs/WIREFRAMES.adoc` - ASCII art wireframes that show engineers the layout and structure of each screen.

## Purpose

Wireframes give engineers visual context for implementation:
- Screen layouts and component placement
- User flows and navigation
- Interaction patterns
- Responsive behavior notes

## Operations

- **Create** - Generate wireframes for new screens/features
- **Edit** - Update existing wireframes
- **View** - Display wireframes for a specific screen

## File Location

```
/docs/WIREFRAMES.adoc
```

## Template

```asciidoc
= Wireframes
:toc:
:icons: font

== Overview

ASCII wireframes for [Project Name] screens. These layouts guide implementation - refer to BRAND_GUIDELINES.adoc for visual styling.

== Screen: [Screen Name]

=== Layout

----
┌─────────────────────────────────────────────────────────┐
│  ┌─────┐                              [User ▼] [Logout] │
│  │LOGO │   Dashboard   Settings   Help                  │
│  └─────┘                                                │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │  Page Title                           [+ Add]   │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Search: [_______________] [Filter ▼] [Search]   │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Name          │ Status   │ Date       │ Actions │   │
│  ├───────────────┼──────────┼────────────┼─────────┤   │
│  │ Item One      │ ● Active │ 2024-01-15 │ ⋮       │   │
│  │ Item Two      │ ○ Draft  │ 2024-01-14 │ ⋮       │   │
│  │ Item Three    │ ● Active │ 2024-01-13 │ ⋮       │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  [< Prev]  Page 1 of 5  [Next >]                       │
│                                                         │
└─────────────────────────────────────────────────────────┘
----

=== Components

[cols="1,3"]
|===
| Component | Notes

| Header
| Fixed top, logo links to home, user dropdown right-aligned

| Search bar
| Debounced input, filter dropdown, search button

| Data table
| Sortable columns, status indicators, actions menu

| Pagination
| Previous/Next with page indicator
|===

=== Interactions

* **Search**: Filters table on Enter or button click (debounce 300ms)
* **Filter dropdown**: Opens filter options, applies on selection
* **Table row hover**: Highlight row, show actions
* **Actions menu (⋮)**: Edit, Duplicate, Delete options
* **Pagination**: Load page, maintain search/filter state
```

## ASCII Art Components Library

### Box Drawing Characters

```
Corners:  ┌ ┐ └ ┘
Lines:    ─ │
T-joins:  ├ ┤ ┬ ┴
Cross:    ┼
Rounded:  ╭ ╮ ╰ ╯ (optional)
Double:   ═ ║ ╔ ╗ ╚ ╝ (for emphasis)
```

### Common UI Elements

#### Buttons
```
[Button]        Primary button
[Cancel]        Secondary button
[× Close]       Close/dismiss button
[+ Add New]     Action with icon
[Save ▼]        Button with dropdown
```

#### Form Inputs
```
[_______________]     Text input
[_____▼]              Dropdown/select
[________________]    Wide input
                |
[               ]     Textarea
[               ]
[_______________]

( ) Option A          Radio buttons
(●) Option B

[ ] Unchecked         Checkboxes
[✓] Checked
```

#### Navigation
```
Tab One | Tab Two | Tab Three       Horizontal tabs

┌──────────┐
│ Menu     │                        Sidebar menu
├──────────┤
│ ▸ Item 1 │
│   Item 2 │
│ ▸ Item 3 │
└──────────┘

[< Back]  Step 2 of 4  [Next >]     Wizard navigation

Home > Category > Page              Breadcrumbs
```

#### Data Display
```
┌──────────┬──────────┬──────────┐
│ Header 1 │ Header 2 │ Header 3 │   Table
├──────────┼──────────┼──────────┤
│ Data     │ Data     │ Data     │
└──────────┴──────────┴──────────┘

┌────────────────────────────────┐
│ Card Title                     │   Card
│                                │
│ Card content goes here        │
│                                │
│              [Action] [Action] │
└────────────────────────────────┘

● Active   ○ Inactive   ◐ Pending    Status indicators

[████████░░] 80%                     Progress bar
```

#### Modals & Overlays
```
┌─────────────────────────────────┐
│ Modal Title                  [×]│
├─────────────────────────────────┤
│                                 │
│  Modal content goes here.       │
│                                 │
│  Are you sure you want to       │
│  delete this item?              │
│                                 │
├─────────────────────────────────┤
│           [Cancel]  [Confirm]   │
└─────────────────────────────────┘
```

#### Messages & Alerts
```
┌─ ℹ Info ─────────────────────────┐
│ This is an informational message │
└──────────────────────────────────┘

┌─ ⚠ Warning ──────────────────────┐
│ This action cannot be undone     │
└──────────────────────────────────┘

┌─ ✓ Success ──────────────────────┐
│ Your changes have been saved     │
└──────────────────────────────────┘

┌─ ✗ Error ────────────────────────┐
│ Something went wrong             │
└──────────────────────────────────┘
```

#### Icons (Text Representations)
```
⋮  More/menu (vertical dots)
⋯  More/menu (horizontal dots)
▼  Dropdown arrow
▸  Expand/submenu
◂  Collapse
✓  Checkmark
✗  Close/error
●  Filled circle (active)
○  Empty circle (inactive)
◐  Half circle (pending)
⚙  Settings
🔍 Search (or use [Search])
+  Add
-  Remove
✎  Edit
🗑 Delete (or use [Delete])
```

### Layout Patterns

#### Header with Navigation
```
┌───────────────────────────────────────────────────────┐
│  LOGO    Nav Item 1   Nav Item 2   Nav Item 3   [User]│
└───────────────────────────────────────────────────────┘
```

#### Sidebar Layout
```
┌────────┬──────────────────────────────────────────────┐
│        │                                              │
│ SIDE   │              MAIN CONTENT                    │
│ BAR    │                                              │
│        │                                              │
│        │                                              │
└────────┴──────────────────────────────────────────────┘
```

#### Form Layout
```
┌────────────────────────────────────────────────────────┐
│ Form Title                                             │
├────────────────────────────────────────────────────────┤
│                                                        │
│  Label 1        [_________________________]            │
│                                                        │
│  Label 2        [_________________________]            │
│                                                        │
│  Label 3        [___________▼]                         │
│                                                        │
│  Label 4        ( ) Option A   (●) Option B            │
│                                                        │
├────────────────────────────────────────────────────────┤
│                          [Cancel]  [Save]              │
└────────────────────────────────────────────────────────┘
```

#### Responsive Notes
```
Desktop (>1024px):     [Sidebar] [Main Content]
Tablet (768-1024px):   [Hamburger] [Full Width Content]
Mobile (<768px):       [Hamburger] [Stacked Content]
```

## Documenting Interactions

For each wireframe, include an interactions section:

```asciidoc
=== Interactions

* **[Element]**: [Action] → [Result]
* **Click [Button]**: Submits form, shows loading state, redirects to X
* **Hover [Row]**: Highlights row, reveals action buttons
* **Focus [Input]**: Shows border highlight, displays helper text
* **Error state**: Red border, error message below input
```

## Linking to User Stories

Reference the User Stories each wireframe implements:

```asciidoc
=== Related User Stories

* US-123: As a user, I want to search items so I can find what I need
* US-124: As a user, I want to filter results so I can narrow my search
* US-125: As a user, I want to paginate results so I can browse large lists
```

## Checklist

Before finalizing wireframes:
- [ ] All screens from Features are covered
- [ ] Layout uses consistent ASCII patterns
- [ ] Component notes explain purpose/behavior
- [ ] Interactions are documented
- [ ] Related User Stories are referenced
- [ ] Responsive behavior is noted (if applicable)
- [ ] Links to BRAND_GUIDELINES.adoc for styling

## Tips

- **Consistent width** - Use same box widths across wireframes
- **Annotate** - Notes are as valuable as the drawings
- **Keep it rough** - Wireframes show structure, not pixel-perfection
- **Show states** - Include empty states, loading, error views
- **Reference stories** - Link wireframes to User Stories they implement
- **Collaborate** - Review wireframes with engineers before implementation
