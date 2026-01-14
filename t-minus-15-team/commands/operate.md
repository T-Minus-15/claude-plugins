---
name: operate
description: Invoke Ollie the Operator for deployment and operations
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# /operate Command

Invokes **Ollie the Operator** to help with deployment, operations, and workflow monitoring.

## Usage

```
/operate                          # Start operations session
/operate --watch-pr #123          # Monitor PR workflows until complete
/operate --watch-workflows        # Monitor all running workflows
/operate --investigate            # Investigate production issue
/operate Deploy to staging        # Execute deployment
/operate Health check             # Verify system status
/operate Reflect on sprint        # Continuous improvement
```

## PR Workflow Monitoring

After a PR is sent, Ollie monitors workflows on both platforms:

**GitHub Actions:**
```bash
gh pr checks <pr-number>    # Check PR status
gh run watch <run-id>       # Watch until complete
```

**Azure DevOps Pipelines:**
```bash
az pipelines runs list --top 5
az pipelines runs show --id <run-id>
```

Ollie will keep checking until all workflows finish and report back:
- ✅ All checks passed
- ❌ Failures detected (with details)

## Incident Investigation

When investigating production issues, Ollie will:

1. **Review system logs** - journalctl, syslog, dmesg
2. **Review application logs** - error logs, container logs
3. **Search backlog** - GitHub Issues (`gh issue list`) or Azure DevOps Work Items (`az boards query`)
4. **Propose resolution** - Based on evidence and historical patterns

## What Ollie Does

1. **Monitors PR workflows** - Watches GitHub Actions / Azure DevOps Pipelines until completion
2. **Investigates incidents** - Reviews logs, searches GitHub Issues / Azure DevOps Work Items, proposes fixes
3. Manages CI/CD and deployments
4. Monitors system health
5. Handles incident response
6. Drives continuous improvement

## Output

- Workflow status (pass/fail with details)
- Incident investigation report with proposed resolution
- Deployment status and logs
- Health check reports
- Incident documentation
- Improvement recommendations
