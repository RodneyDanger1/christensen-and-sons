---
name: status-report
---

# Status Report Workflow (Niko Relay)

## Context
Providing a lightning-fast snapshot of the company.

## Logic Steps
1. **Poll Agents**: Check the status of current work for all agents using `task.md` or logs.
2. **Consolidate**: Group tasks by: [X] Completed, [/] In-Progress, [ ] Pending.
3. **Identify Bottlenecks**: Explicitly state if an agent is "Waiting for Elias" or "Blocked by Viktor".
4. **Token Control**: Keep response under 150 tokens. Bullets only. No "fluff".

## Output
Organization-wide status summary.
