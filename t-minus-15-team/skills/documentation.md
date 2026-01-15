---
name: documentation
description: Standard documentation structure for T-Minus-15 projects. Defines the /docs folder layout and AsciiDoc templates.
allowed-tools: Read, Write, Edit, Glob, Grep, AskUserQuestion
---

# Documentation Skill

This skill defines the standard documentation structure for T-Minus-15 projects. All project documentation lives in the `/docs` folder using AsciiDoc format.

## Documentation Structure

| File | Purpose | Primary Owner |
|------|---------|---------------|
| `SOLUTION_DESIGN.adoc` | High-level architecture and design decisions | Archie |
| `DATA_MODEL.adoc` | Database schema, entities, relationships | Archie, Pennie |
| `TESTING.adoc` | Test strategy, coverage requirements, testing approach | Teddie |
| `DEPLOYMENT.adoc` | Deployment procedures (for hosted/cloud applications) | Ollie |
| `INSTALLATION.adoc` | Installation guide (for on-premise/local applications) | Ollie, Ernie |
| `CONFIDENTIALITY.adoc` | Data classification, security requirements, access controls | Archie |
| `CONTACTS.adoc` | Key stakeholders, support contacts, escalation paths | Poppie |
| `FAQS.adoc` | Frequently asked questions and answers | Poppie, Pennie |
| `TERMS.adoc` | Glossary of domain-specific terms and definitions | Pennie |
| `ACRONYMS.adoc` | Project and industry acronyms | Pennie |
| `TROUBLESHOOTING.adoc` | Common problems and solutions (table format) | Ollie, Teddie |
| `TECHNICAL_SOLUTION.adoc` | Master document that compiles all above docs | Archie, Connie |

### Support Files

| File | Purpose |
|------|---------|
| `includes/document-history.adoc` | Auto-generated version history from git |
| `includes/project-features-table.adoc` | Feature list linked to DevOps work items |

## When to Use Each Document

### DEPLOYMENT.adoc vs INSTALLATION.adoc

Choose based on application type:

- **DEPLOYMENT.adoc** - Cloud/hosted applications (Azure, AWS, etc.)
  - CI/CD pipelines
  - Environment configuration
  - Release processes

- **INSTALLATION.adoc** - On-premise/local applications
  - System requirements
  - Step-by-step installation
  - Configuration files

## Document Templates

### DATA_MODEL.adoc

```asciidoc
= Data Model
:toc: left
:toclevels: 3
:sectnums:

== Overview

Brief description of the data architecture, entity relationships, and data flows.

== Entity Definitions

=== Entity Name

[cols="2,2,2,1,1,1,3",options="header"]
|===
| UI Label | Model Field | DB Column | Type | Unit | Editable | Source/Formula

| ID
| id
| id
| UUID
| -
| No
| Auto-generated

| Name
| name
| name
| String
| -
| Yes
| User input

| Total
| total
| total
| Decimal
| £
| No
| `SUM(line_items.amount)`

|===

**Notes:**
- Editable = Yes means user can modify via UI
- Editable = No means calculated or system-generated
- Source/Formula column documents data origin or calculation

== Relationships

[mermaid]
----
erDiagram
    ENTITY1 ||--o{ ENTITY2 : "has many"
    ENTITY2 }|--|| ENTITY3 : "belongs to"
----

== Dropdown/Lookup Sources

Document where dropdown options come from:

| Dropdown | Source Table | Filter | Display Field |
|----------|--------------|--------|---------------|
| Status | StatusCodes | Active='Y' | Description |
| Category | Categories | - | Name |
```

### TESTING.adoc

```asciidoc
= Test Strategy
:toc:
:sectnums:

== Overview

Testing approach and philosophy.

== Test Types

=== Unit Tests

- Framework: [Vitest/Jest/etc.]
- Location: `/tests/unit/`
- Coverage target: [X%]

=== Integration Tests

- Framework: [specify]
- Location: `/tests/integration/`

=== E2E Tests

- Framework: Playwright
- Location: `/tests/e2e/`

== Running Tests

[source,bash]
----
bun test           # Unit tests
bun test:e2e       # E2E tests
----
```

### SOLUTION_DESIGN.adoc

```asciidoc
= Solution Design
:toc:
:sectnums:

== Overview

High-level description of the solution.

== Architecture

[mermaid]
----
flowchart TB
    subgraph Frontend
        UI[Web UI]
    end
    subgraph Backend
        API[API Server]
        DB[(Database)]
    end
    UI --> API --> DB
----

== Technology Stack

[cols="1,2"]
|===
| Component | Technology

| Frontend
| Next.js, React, TypeScript

|===

== Design Decisions

=== Decision 1

**Context:** [Why this decision was needed]

**Decision:** [What was decided]

**Rationale:** [Why this approach]
```

### DEPLOYMENT.adoc

```asciidoc
= Deployment Guide
:toc:
:sectnums:

== Environments

[cols="1,1,2"]
|===
| Environment | URL | Purpose

| Development
| dev.example.com
| Development testing

| Staging
| staging.example.com
| Pre-production validation

| Production
| example.com
| Live environment

|===

== CI/CD Pipeline

Deployment process overview.

== Environment Variables

[cols="1,2,1"]
|===
| Variable | Description | Required

| DATABASE_URL
| Database connection string
| Yes

|===
```

### INSTALLATION.adoc

```asciidoc
= Installation Guide
:toc:
:sectnums:

== System Requirements

- OS: [Windows/Linux/macOS]
- Memory: [minimum RAM]
- Disk: [minimum storage]

== Prerequisites

- Node.js v20+
- [Other dependencies]

== Installation Steps

. Download the application
. Extract to installation directory
. Configure environment
. Run installation script

[source,bash]
----
./install.sh
----

== Configuration

Configuration file location: `/etc/app/config.yaml`
```

### CONFIDENTIALITY.adoc

```asciidoc
= Confidentiality & Security
:toc:
:sectnums:

== Data Classification

[cols="1,2,2"]
|===
| Classification | Description | Handling

| Public
| Non-sensitive information
| No restrictions

| Internal
| Business information
| Internal access only

| Confidential
| Sensitive data
| Restricted access, encrypted

|===

== Access Controls

Who can access what and why.

== Compliance

Relevant compliance requirements (GDPR, SOC2, etc.)
```

### CONTACTS.adoc

```asciidoc
= Contacts
:toc:

== Project Team

[cols="1,1,1,1"]
|===
| Role | Name | Email | Phone

| Project Lead
|
|
|

| Technical Lead
|
|
|

|===

== Support

[cols="1,2"]
|===
| Type | Contact

| General Support
| support@example.com

| Emergency
| +44 xxx xxx xxxx

|===

== Escalation Path

. First contact: Support team
. Escalate to: Technical Lead
. Final escalation: Project Lead
```

### FAQS.adoc

```asciidoc
= Frequently Asked Questions
:toc:

== General

=== Question 1?

Answer to question 1.

=== Question 2?

Answer to question 2.

== Technical

=== How do I...?

Step-by-step answer.
```

### ACRONYMS.adoc

```asciidoc
= Acronyms
:toc:

Project and industry acronyms used in this documentation.

== General Technical

[cols="1,3"]
|===
| Acronym | Definition

| API
| Application Programming Interface

| CI/CD
| Continuous Integration / Continuous Deployment

| CRUD
| Create, Read, Update, Delete

| UI/UX
| User Interface / User Experience

|===

== Project Specific

[cols="1,3"]
|===
| Acronym | Definition

| BOM
| Bill of Materials

| [Add project-specific acronyms as they are encountered]
|

|===

== Industry / Domain

[cols="1,3"]
|===
| Acronym | Definition

| [Add industry acronyms as they are encountered]
|

|===
```

**Pennie's Responsibility:** Pennie should add acronyms to this file whenever she encounters them during:
- Transcript reviews
- Stakeholder conversations
- Document analysis
- Backlog reviews

### TERMS.adoc

```asciidoc
= Glossary of Terms
:toc:

Domain-specific terms and definitions (not acronyms - see ACRONYMS.adoc).

== Domain Terms

[cols="1,3"]
|===
| Term | Definition

| [Term]
| [Definition]

|===

== Business Terms

[cols="1,3"]
|===
| Term | Definition

| [Term]
| [Definition]

|===
```

### TROUBLESHOOTING.adoc

```asciidoc
= Troubleshooting Guide

[cols="2,3"]
|===
| Problem | Solution

| Application fails to start
| Check database connection string in environment variables

| Authentication errors
| Verify API keys are correctly configured

| Slow performance
| Check database indexes and connection pool settings

|===
```

### TECHNICAL_SOLUTION.adoc

```asciidoc
= Technical Solution Design - [Project Name]
[Client Name]
:doctype: book
:toc: left
:toclevels: 2
:sectlinks:
:sectanchors:
:sectnums!:
:source-highlighter: highlight.js
:icons: font
:imagesdir: images

// Front matter (before numbered sections)
include::TERMS.adoc[]

include::CONFIDENTIALITY.adoc[]

== Document Information

[cols="1,2",options="header"]
|===
|Attribute |Value

|Document Title |Technical Solution Design - [Project Name]
|Version |1.0
|Status |Draft
|Author |[Author]
|Client |[Client Name]
|Epic Reference |[Epic ID]
|===

== Document History

include::includes/document-history.adoc[]

// Main content (numbered sections)
:sectnums:
include::SOLUTION_DESIGN.adoc[]

include::DATA_MODEL.adoc[]

include::TESTING.adoc[]

include::DEPLOYMENT.adoc[]

// Appendices
[appendix]
include::TROUBLESHOOTING.adoc[]

[appendix]
include::FAQS.adoc[]

[appendix]
include::CONTACTS.adoc[]
```

### includes/document-history.adoc

```asciidoc
// Auto-generated Document History from Git commits
// DO NOT EDIT THIS FILE MANUALLY - it will be overwritten
// To regenerate: ./scripts/generate-document-history.sh

[cols="1,2,2,4",options="header"]
|===
|Version |Date |Author |Changes

|1.0 |DD-MM-YYYY |[Author] |Initial documentation
|===
```

## Usage

### Creating Documentation

When starting a new project, create the `/docs` folder and initialise the relevant documents:

```bash
mkdir -p docs
```

### Choosing Documents

Not all projects need all documents. At minimum, consider:

1. **SOLUTION_DESIGN.adoc** - Always needed
2. **DATA_MODEL.adoc** - If the project has a database
3. **DEPLOYMENT.adoc** or **INSTALLATION.adoc** - Based on app type
4. **TESTING.adoc** - Always needed
5. **TROUBLESHOOTING.adoc** - Build as issues arise

### Generating PDFs

Use the `generate-docs.sh` script (see Archie's documentation):

```bash
cd docs && ./generate-docs.sh
```

## Tips

- Keep documents focused - one topic per file
- Use Mermaid diagrams for visual clarity
- Update documentation as part of the development process
- TECHNICAL_SOLUTION.adoc compiles everything - useful for handovers
- Add to TROUBLESHOOTING.adoc whenever you solve a new problem
