---
name: risk
description: Create, edit, and manage Risk work items. Risks are potential future problems that may impact delivery.
tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion
---

# Risk Skill

Create and manage Risk work items following T-Minus-15 methodology. Risks are potential future problems that may impact delivery if not mitigated.

## Definition

**Risk**: A potential future problem that may impact delivery. Risks are identified early and require mitigation plans before they become Issues.

**Key Distinction**:
- **Risk** = Potential problem (hasn't happened yet)
- **Issue** = Current problem (already happening)

## Risk vs Issue

| Aspect | Risk | Issue |
|--------|------|-------|
| Timing | Future/potential | Current/active |
| Action | Mitigation plan | Resolution |
| Owner | Poppie (planning) | Assigned agent |
| Urgency | Proactive | Reactive |

## Risk Severity

| Severity | Probability | Impact | Example |
|----------|-------------|--------|---------|
| **High** | Likely | Major impact | Third-party API may have rate limits |
| **Medium** | Possible | Moderate impact | Team member may be unavailable |
| **Low** | Unlikely | Minor impact | Minor browser compatibility issues |

## Risk Template

### Required Fields

| Field | Description | Required |
|-------|-------------|----------|
| Title | Clear description of the potential problem | Yes |
| Severity | High/Medium/Low | Yes |
| Probability | Likelihood of occurring | Yes |
| Impact | What happens if it occurs | Yes |
| Mitigation Plan | Steps to reduce probability or impact | Yes |
| Owner | Person responsible for monitoring | Yes |

### Optional Fields

| Field | Description |
|-------|-------------|
| Related Feature | Feature this risk affects |
| Trigger | What would cause this risk to become an Issue |
| Contingency | Backup plan if mitigation fails |
| Review Date | When to reassess the risk |

## Azure DevOps

### Check Process Template

```bash
# Get project process template
az devops project show --project "<project>" --query "capabilities.processTemplate.templateName" -o tsv

# List available work item types
az boards work-item type list --project "<project>" --query "[].name" -o tsv
```

**Process Templates:**
- **Agile**: No native Risk type - use Issue with tag "Risk"
- **Scrum**: No native Risk type - use Impediment with tag "Risk"
- **CMMI**: Risk (native work item type)
- **Basic**: No native Risk type - use Issue with tag "Risk"

### Create Risk (CMMI)

```bash
# CMMI process has native Risk type
az boards work-item create \
  --type "Risk" \
  --title "Third-party API may have rate limits" \
  --project "<project>" \
  --fields "Microsoft.VSTS.Common.Severity=2 - High" \
           "Microsoft.VSTS.CMMI.Probability=70" \
           "Microsoft.VSTS.Common.RootCause=External dependency"
```

### Create Risk (Non-CMMI)

```bash
# Use Issue with Risk tag for Agile/Scrum/Basic
az boards work-item create \
  --type "Issue" \
  --title "[Risk] Third-party API may have rate limits" \
  --project "<project>" \
  --fields "System.Tags=Risk,High-Priority" \
           "System.Description=<html><h2>Probability</h2><p>High - 70%</p><h2>Impact</h2><p>Feature delivery delayed</p><h2>Mitigation</h2><p>Implement caching layer</p></html>"
```

### Query Risks

```bash
# CMMI - native Risk type
az boards query --wiql "SELECT [ID], [Title], [Severity], [State] FROM WorkItems WHERE [Work Item Type] = 'Risk' AND [State] <> 'Closed'" -o table

# Other templates - tagged Issues
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Tags] CONTAINS 'Risk' AND [State] <> 'Closed'" -o table

# High severity risks
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Tags] CONTAINS 'Risk' AND [Tags] CONTAINS 'High-Priority' AND [State] <> 'Closed'"
```

## GitHub

GitHub uses Issues with labels for risk tracking.

### Create Risk Issue

```bash
gh issue create \
  --title "[Risk] Third-party API may have rate limits" \
  --body "## Severity
High

## Probability
70% - Likely based on vendor documentation

## Impact
If rate limits are hit during peak usage:
- Feature requests will fail
- User experience degraded
- Potential data loss

## Mitigation Plan
1. Implement request caching layer
2. Add retry logic with exponential backoff
3. Set up monitoring for API usage
4. Contact vendor about enterprise limits

## Owner
@poppie

## Related Feature
#<feature-issue-number>

## Trigger
API returns 429 status codes during testing

## Contingency
Fall back to local queue with batch processing

## Review Date
Before Feature moves to Engineer phase" \
  --label "risk,high-priority"
```

### Query Risks

```bash
# All open risks
gh issue list --label "risk" --state open

# High priority risks
gh issue list --label "risk,high-priority" --state open

# Risks for current milestone
gh issue list --label "risk" --milestone "Sprint 5"
```

## Risk Management Lifecycle

### 1. Identification

Risks are identified during:
- Sprint planning
- Feature breakdown
- Design reviews
- Technical spikes

### 2. Assessment

For each risk, evaluate:
- **Probability**: How likely is it to occur?
- **Impact**: What's the damage if it does?
- **Detectability**: How early can we detect it?

### 3. Mitigation Planning

Choose a strategy:
| Strategy | Description | When to Use |
|----------|-------------|-------------|
| **Avoid** | Eliminate the risk entirely | High impact, high probability |
| **Reduce** | Lower probability or impact | Medium risks |
| **Transfer** | Shift to third party (insurance, contracts) | Financial risks |
| **Accept** | Acknowledge and monitor | Low impact risks |

### 4. Monitoring

- Review risks at sprint boundaries
- Update probability as information changes
- Escalate if risk becomes Issue
- Close risks that are no longer relevant

## Risk Review Checklist

Before closing a risk:
- [ ] Risk is no longer applicable OR
- [ ] Risk has been fully mitigated OR
- [ ] Risk has converted to Issue (create Issue, close Risk)
- [ ] Lessons learned documented
- [ ] Related work items updated

## Risk to Issue Conversion

When a risk materializes:

```bash
# Azure DevOps
az boards work-item create \
  --type "Issue" \
  --title "API rate limits exceeded - was Risk #<id>" \
  --project "<project>" \
  --fields "System.Description=Risk #<id> has materialized. Implementing contingency plan."

# Close the original risk
az boards work-item update \
  --id <risk-id> \
  --fields "System.State=Closed" \
           "System.Reason=Risk materialized - see Issue #<id>"
```

```bash
# GitHub
gh issue create \
  --title "[Issue] API rate limits exceeded - was Risk #<number>" \
  --body "Risk #<number> has materialized. Implementing contingency plan."

# Close the original risk
gh issue close <risk-number> --comment "Risk materialized - see Issue #<new-number>"
```

## Tips

- **Identify early** - Risks found early are cheaper to mitigate
- **Be specific** - "Something might go wrong" is not a risk
- **Own it** - Every risk needs an owner
- **Review regularly** - Risks change as projects progress
- **Don't over-document** - Focus on high-impact risks
- **Convert promptly** - When risk becomes Issue, act immediately
