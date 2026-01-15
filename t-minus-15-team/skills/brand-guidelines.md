---
name: brand-guidelines
description: Create and maintain brand guidelines documentation. Defines colors, typography, spacing, and reusable components for consistent UI implementation.
tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion
---

# Brand Guidelines Skill

Create and maintain `/docs/BRAND_GUIDELINES.adoc` - the visual design system that ensures consistent UI implementation across the project.

## Purpose

Brand guidelines give engineers the visual specifications they need to implement UI without guessing:
- Color values (hex codes, usage)
- Typography (font families, sizes, weights)
- Spacing scale (consistent padding/margins)
- Component specifications (buttons, cards, forms, etc.)

## Workflow

**IMPORTANT:** Always follow this decision flow:

```
┌─────────────────────────────────────────────────────────┐
│  Step 1: Ask for existing brand guidelines              │
│                                                         │
│  "Do you have existing brand guidelines I can use?      │
│   (PDF, style guide, Figma exports, etc.)"              │
└─────────────────────────┬───────────────────────────────┘
                          │
            ┌─────────────┴─────────────┐
            │                           │
            ▼                           ▼
    ┌───────────────┐          ┌───────────────────┐
    │  YES - User   │          │  NO - No existing │
    │  provides doc │          │  guidelines       │
    └───────┬───────┘          └─────────┬─────────┘
            │                            │
            ▼                            ▼
    ┌───────────────┐          ┌───────────────────┐
    │ Extract from  │          │ Step 2: Ask for   │
    │ provided docs │          │ customer website  │
    │ into template │          │                   │
    └───────────────┘          │ "What is the      │
                               │ customer's        │
                               │ website URL?"     │
                               └─────────┬─────────┘
                                         │
                                         ▼
                               ┌───────────────────┐
                               │ Step 3: Extract   │
                               │ styles from site  │
                               │ using Chrome ext  │
                               └───────────────────┘
```

### Step 1: Ask for Existing Guidelines

```
AskUserQuestion:
  question: "Do you have existing brand guidelines I can use? (PDF, style guide, design system documentation)"
  options:
    - "Yes, I'll provide them"
    - "No, extract from our website"
    - "No, create from scratch"
```

### Step 2: If No Guidelines, Get Website URL

```
AskUserQuestion:
  question: "What is the customer's website URL so I can extract their brand styles?"
```

### Step 3: Extract from Website

Use Chrome extension to navigate to the site and extract styles (see Extraction section below).

## Operations

- **Create** - Generate new brand guidelines from existing docs or by extracting from website
- **Edit** - Update specific sections (colors, typography, components)
- **View** - Display current brand guidelines

## File Location

```
/docs/BRAND_GUIDELINES.adoc
```

## Template

```asciidoc
= Brand Guidelines
:toc:
:icons: font

== Overview

[Brief description of the brand identity and design principles]

== Color Palette

=== Primary Colors

[cols="1,2,3"]
|===
| Swatch | Value | Usage

| [.primary]#████#
| `#0066CC`
| Primary actions, links, focus states

| [.primary-dark]#████#
| `#004499`
| Primary hover/active states
|===

=== Secondary Colors

[cols="1,2,3"]
|===
| Swatch | Value | Usage

| [.secondary]#████#
| `#6C757D`
| Secondary buttons, muted text
|===

=== Semantic Colors

[cols="1,2,3"]
|===
| Swatch | Value | Usage

| [.success]#████#
| `#28A745`
| Success messages, confirmations

| [.warning]#████#
| `#FFC107`
| Warnings, caution states

| [.error]#████#
| `#DC3545`
| Errors, destructive actions

| [.info]#████#
| `#17A2B8`
| Informational messages
|===

=== Neutral Colors

[cols="1,2,3"]
|===
| Swatch | Value | Usage

| [.white]#████#
| `#FFFFFF`
| Backgrounds, cards

| [.gray-100]#████#
| `#F8F9FA`
| Page backgrounds

| [.gray-300]#████#
| `#DEE2E6`
| Borders, dividers

| [.gray-600]#████#
| `#6C757D`
| Muted text, placeholders

| [.gray-900]#████#
| `#212529`
| Primary text
|===

== Typography

=== Font Families

[cols="1,2,3"]
|===
| Usage | Font Stack | Fallback

| Headings
| `Inter`
| `-apple-system, BlinkMacSystemFont, sans-serif`

| Body
| `Open Sans`
| `system-ui, sans-serif`

| Code
| `Fira Code`
| `Consolas, Monaco, monospace`
|===

=== Font Scale

[cols="1,1,1,2"]
|===
| Element | Size | Weight | Line Height

| H1
| `2.5rem` (40px)
| 700
| 1.2

| H2
| `2rem` (32px)
| 600
| 1.25

| H3
| `1.5rem` (24px)
| 600
| 1.3

| H4
| `1.25rem` (20px)
| 600
| 1.4

| Body
| `1rem` (16px)
| 400
| 1.5

| Small
| `0.875rem` (14px)
| 400
| 1.5

| Caption
| `0.75rem` (12px)
| 400
| 1.4
|===

== Spacing

=== Spacing Scale

Use consistent spacing values based on 4px base unit:

[cols="1,2,2"]
|===
| Token | Value | Usage

| `xs`
| `0.25rem` (4px)
| Tight spacing, icon gaps

| `sm`
| `0.5rem` (8px)
| Button padding, list items

| `md`
| `1rem` (16px)
| Default spacing, form gaps

| `lg`
| `1.5rem` (24px)
| Section spacing

| `xl`
| `2rem` (32px)
| Large section spacing

| `2xl`
| `3rem` (48px)
| Page section spacing
|===

== Components

=== Buttons

[cols="1,3"]
|===
| Variant | Specification

| Primary
| Background: Primary color, Text: White, Border-radius: 4px, Padding: 8px 16px

| Secondary
| Background: Transparent, Text: Primary color, Border: 1px solid Primary, Border-radius: 4px

| Danger
| Background: Error color, Text: White, Border-radius: 4px

| Disabled
| Background: Gray-300, Text: Gray-600, Cursor: not-allowed
|===

**States:**
- Hover: Darken background 10%
- Active: Darken background 15%
- Focus: 2px outline offset 2px in Primary color

=== Form Inputs

[cols="1,2"]
|===
| Property | Value

| Border
| 1px solid Gray-300

| Border-radius
| 4px

| Padding
| 8px 12px

| Font-size
| 1rem

| Focus border
| Primary color

| Error border
| Error color

| Placeholder color
| Gray-600
|===

=== Cards

[cols="1,2"]
|===
| Property | Value

| Background
| White

| Border-radius
| 8px

| Shadow
| `0 2px 4px rgba(0,0,0,0.1)`

| Padding
| 1.5rem (24px)

| Border
| 1px solid Gray-100 (optional)
|===

=== Tables

[cols="1,2"]
|===
| Property | Value

| Header background
| Gray-100

| Header text
| Gray-900, font-weight 600

| Row border
| 1px solid Gray-300

| Cell padding
| 12px 16px

| Hover row
| Gray-100 background
|===

== Icons

=== Icon Library

[Specify icon library: Heroicons, Feather Icons, Material Icons, etc.]

=== Icon Sizes

[cols="1,2,2"]
|===
| Size | Dimensions | Usage

| Small
| 16x16px
| Inline with text, buttons

| Medium
| 24x24px
| Navigation, list items

| Large
| 32x32px
| Feature highlights
|===

== Accessibility

=== Color Contrast

- Normal text: Minimum 4.5:1 contrast ratio
- Large text (18px+): Minimum 3:1 contrast ratio
- UI components: Minimum 3:1 contrast ratio

=== Focus Indicators

All interactive elements must have visible focus indicators:
- Outline: 2px solid Primary color
- Outline-offset: 2px

=== Motion

- Respect `prefers-reduced-motion` media query
- Default transition: 150ms ease-in-out
```

## Extraction from Existing Site

If no brand guidelines exist, Dannie can extract styles from an existing website using the Chrome extension:

### Colors
```javascript
// Get CSS custom properties
JSON.stringify(Object.fromEntries(
  Array.from(document.styleSheets)
    .flatMap(s => { try { return Array.from(s.cssRules) } catch { return [] }})
    .filter(r => r.style?.cssText?.includes('--'))
    .slice(0, 20)
    .map(r => [r.selectorText, r.style.cssText])
))
```

### Typography
```javascript
// Get font families
getComputedStyle(document.body).fontFamily + ' | ' +
getComputedStyle(document.querySelector('h1') || document.body).fontFamily
```

### Color Sampling
```javascript
// Get common colors
JSON.stringify({
  background: getComputedStyle(document.body).backgroundColor,
  text: getComputedStyle(document.body).color,
  primary: getComputedStyle(document.querySelector('a, button, [class*="primary"]') || document.body).backgroundColor,
  heading: getComputedStyle(document.querySelector('h1, h2') || document.body).color
})
```

## Checklist

Before finalizing brand guidelines:
- [ ] Primary and secondary colors defined with hex values
- [ ] Semantic colors (success, warning, error, info) defined
- [ ] Neutral color scale defined
- [ ] Font families specified with fallbacks
- [ ] Font scale defined for headings and body
- [ ] Spacing scale defined
- [ ] Button variants and states specified
- [ ] Form input styles defined
- [ ] Card/container styles defined
- [ ] Accessibility requirements documented
- [ ] Icon library and sizes specified

## Tips

- **Hex codes always** - Engineers need exact values, not color names
- **Include states** - Hover, active, focus, disabled for all interactive elements
- **Spacing consistency** - Use a scale (4px base) rather than arbitrary values
- **Accessibility first** - Ensure contrast ratios meet WCAG guidelines
- **Less is more** - A small, consistent palette is better than many colors
