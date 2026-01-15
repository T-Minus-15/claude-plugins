---
name: copy
description: Invoke Connie the Copywriter to review documentation quality
allowed-tools: Read, Grep, Glob, Write, Edit, Task, AskUserQuestion
---

# /copy Command

Invokes **Connie the Copywriter** to review documentation for quality, consistency, and professional tone.

## Usage

```
/copy                    # Review all docs in /docs folder
/copy SOLUTION_DESIGN    # Review specific document
/copy --all              # Full review of all documentation
```

## What Connie Checks

- **Spelling & Grammar** - Typos, punctuation, Oxford spelling (-ize)
- **Tone & Style** - Professional, consistent, active voice
- **Structure** - Logical flow, not just bullet lists
- **Completeness** - No placeholder text, all sections filled
- **Terminology** - Consistent terms, acronyms defined

## Delegation

Connie delegates updates to the appropriate agent:
- TESTING.adoc → Teddie
- DEPLOYMENT.adoc → Ollie
- SOLUTION_DESIGN.adoc → Archie
- DATA_MODEL.adoc → Archie/Pennie
- FAQS.adoc → Poppie

## When to Use

- Before client handover
- Before PR that includes documentation
- After major documentation updates
- As part of release checklist
