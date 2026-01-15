---
name: lean-business-case
description: Create lean business cases for Epics following T-Minus-15 methodology. Covers value statement, business outcome hypothesis, leading indicators, and return analysis.
allowed-tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion, WebFetch, WebSearch
---

# Lean Business Case Skill

Create compelling business cases for Epics following T-Minus-15 methodology. A lean business case justifies the investment and defines measurable success criteria.

**Reference:** [T-Minus-15 Epic Metadata](https://github.com/T-Minus-15/book/blob/main/appendices/epic-metadata.adoc)

## Purpose

A lean business case answers:
- **Why** should we do this? (Value Statement)
- **What** does success look like? (Business Outcome Hypothesis)
- **How** will we know we're on track? (Leading Indicators)
- **What's** the return? (ROI/Business Impact)

## Business Case Components

### 1. Value Statement (Elevator Pitch)

**Format:**
```
FOR [target users/customers]
WHO [have this need/problem]
THE [solution name]
IS A [category/type of solution]
THAT [key benefit/value proposition]
UNLIKE [current alternatives]
OUR SOLUTION [key differentiator]
```

**Word Count:** 30-200 words

**Example:**
```
FOR manufacturing engineers
WHO need efficient BOM management with accurate calculations
THE React BOM App
IS A modern web application
THAT provides responsive UI, real-time calculated fields, and ERP integration
UNLIKE the current Power App which is slow and difficult to maintain
OUR SOLUTION offers improved performance, easier maintenance, and better developer experience
```

**Questions to Ask:**
- "Who specifically will use this?" (Be specific - not just "users")
- "What problem are they facing today?"
- "What makes our approach different from alternatives?"

### 2. Business Outcome Hypothesis

**Purpose:** Define how success will be measured. What business outcomes are expected?

**Word Count:** 30-200 words

**Format:**
```
Success will be measured by:
1. [Quantifiable outcome 1]
2. [Quantifiable outcome 2]
3. [Quantifiable outcome 3]
```

**Example:**
```
Success will be measured by:
1. Zero calculation discrepancies vs current Power App
2. Page load times under 2 seconds (currently 8+ seconds)
3. User adoption rate >90% within 30 days of launch
4. 50% reduction in maintenance overhead for IT team
5. Developer onboarding time reduced from 2 weeks to 2 days
```

**Questions to Ask:**
- "How will we know this Epic succeeded?"
- "What metrics matter to the business?"
- "What would failure look like?"

**IMPORTANT:** Only include percentages or numbers if you have data to support them. Avoid made-up metrics.

### 3. Leading Indicators

**Purpose:** Tangible, measurable indicators that predict success BEFORE outcomes are realized.

**Word Count:** 30-200 words

**Format:**
```
We will track these leading indicators:
- [Indicator 1]: [Target] (measured by [method])
- [Indicator 2]: [Target] (measured by [method])
- [Indicator 3]: [Target] (measured by [method])
```

**Example:**
```
We will track these leading indicators:
- Development velocity: Story points per sprint trending upward
- Test coverage: >80% for calculation engine before release
- User feedback: Positive sentiment in UAT sessions (weekly surveys)
- Performance benchmarks: Sub-second response times in dev environment
- Defect rate: <5 bugs per Feature during testing phase
```

**Good Leading Indicators:**
- Can be measured during development (not just after launch)
- Predict final outcomes
- Are actionable (if indicator is bad, we can adjust)

**Bad Leading Indicators:**
- Only measurable after launch
- Vanity metrics that don't predict success
- Things outside our control

### 4. Return Analysis

**Purpose:** Financial or strategic benefits expected from the investment.

**Word Count:** 30-200 words

#### Quantifiable Returns
```
- Cost savings: [Amount/percentage] through [mechanism]
- Revenue increase: [Amount/percentage] from [source]
- Time savings: [Hours/days] per [period] for [who]
- Risk reduction: [What risk] reduced by [how much]
```

#### Strategic Returns
```
- Market positioning: [How this improves competitive position]
- Capability building: [New capabilities enabled]
- Technical debt reduction: [What debt is addressed]
- Compliance: [Regulatory requirements met]
```

**Example:**
```
Quantifiable Returns:
- Maintenance cost reduction: ~40% ($X/year) by moving from Power Platform to React
- User productivity: 2 hours/week saved per engineer (faster load times)
- Development velocity: 3x faster feature delivery with modern stack

Strategic Returns:
- Technical debt elimination: Remove dependency on legacy Power App
- Developer experience: Attract and retain talent with modern tech stack
- Scalability: Architecture supports future feature expansion
```

### 5. Anticipated Business Impact

**Purpose:** Expected effects on business operations, revenue, reputation.

**Word Count:** 50-200 words

**Areas to Address:**
- Operations impact
- Revenue/cost impact
- Reputation/brand impact
- Risk impact
- Capability impact

**Example:**
```
This Epic will impact the business in the following ways:

Operations: Manufacturing engineers will complete BOM management tasks 50% faster,
reducing bottlenecks in the production planning process.

Cost: Reduced maintenance overhead frees IT resources for higher-value work.
Estimated savings of $X/year in support costs.

Risk: Eliminates single point of failure (current Power App maintainer).
Multiple developers can now support the application.

Capability: Modern architecture enables future integration with additional
ERP systems and expansion to other manufacturing sites.
```

## Lean Business Case Template

```markdown
## Business Case: [Epic Name]

### Value Statement
FOR [target]
WHO [need]
THE [solution]
IS A [category]
THAT [benefit]
UNLIKE [alternatives]
OUR SOLUTION [differentiator]

### Business Outcome Hypothesis
Success will be measured by:
1. [Outcome 1]
2. [Outcome 2]
3. [Outcome 3]

### Leading Indicators
- [Indicator 1]: [Target]
- [Indicator 2]: [Target]
- [Indicator 3]: [Target]

### Return Analysis
**Quantifiable:**
- [Return 1]
- [Return 2]

**Strategic:**
- [Return 1]
- [Return 2]

### Anticipated Business Impact
[50-200 words on operations, cost, risk, capability impacts]

### Investment Required
- Estimated effort: [X] story points / [Y] sprints
- Team: [Roles needed]
- Dependencies: [External dependencies]

### Recommendation
[Go / No-Go / Conditional] - [Brief rationale]
```

## Questions Pennie Should Ask

### For Value Statement
- "Who exactly will use this? Can you name specific roles or people?"
- "What problem are they facing today? How painful is it?"
- "What alternatives exist? Why aren't they sufficient?"
- "What makes our approach unique?"

### For Business Outcomes
- "How will the business know this succeeded?"
- "What metrics does leadership care about?"
- "What would make this Epic a failure?"
- "Are there contractual or regulatory requirements to meet?"

### For Leading Indicators
- "What can we measure during development to know we're on track?"
- "What early warning signs should we watch for?"
- "How often should we check these indicators?"

### For Return Analysis
- "What's the cost of NOT doing this?"
- "Are there hard cost savings or soft benefits?"
- "What's the payback period expectation?"
- "Are there strategic benefits beyond cost?"

### For Business Impact
- "Which departments/teams are affected?"
- "Are there downstream systems or processes impacted?"
- "What risks does this mitigate or introduce?"

## Validation Checklist

Before finalizing a business case:
- [ ] Value Statement follows FOR/WHO/THE/IS A/THAT format
- [ ] Target users are specific (not generic "users")
- [ ] Problem statement is clear and validated
- [ ] Business outcomes are measurable
- [ ] Leading indicators can be tracked during development
- [ ] Return analysis has realistic numbers (or acknowledges estimates)
- [ ] Business impact covers operations, cost, risk
- [ ] No made-up percentages without supporting data
- [ ] Stakeholders have reviewed and agreed

## Tips

- **Be specific** - "Manufacturing engineers" not "users"
- **Be honest** - Don't invent metrics; say "estimated" if unsure
- **Be measurable** - If you can't measure it, reconsider it
- **Be realistic** - Overpromising damages credibility
- **Research first** - Understand the company and domain before writing
- **Validate assumptions** - Ask stakeholders if your understanding is correct
