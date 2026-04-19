---
name: hire-agents
---

# Agent Hiring Workflow (Marcus Christensen)

## Context
Determines when and how to scale horizontally using Gemini Flash workers.

## Logic Steps
1. **Grunt-Work Assessment**: Identify batch/low-stakes tasks.
2. **Flash Mandate**: Write hyper-focused instructions for the worker.
3. **Resource Capping**: Set token limits and completion targets.
4. **Handoff**: Dispatch worker mandate to Niko Relay.

## Output
A Flash Worker Mandate (JSON or Markdown).
