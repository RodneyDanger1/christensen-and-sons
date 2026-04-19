---
name: task-routing
---

# Task Routing Workflow (Niko Relay)

## Context
Receiving input from Marcus and assigning it to the right specialist.

## Model Grounding (Gemma 4)
- **Extreme Speed**: Aim for sub-second analysis. 
- **Ambiguity Detection**: If a task is "Ask Viktor to fix it," you must ask "Fix what?" and check the logs before routing.

## Logic Steps
1. **Analyze Input**: Determine the primary intent (Build? Audit? Research?).
2. **Specialist Selection**:
    - **Engineering (Build/Fix)**: Viktor Forge.
    - **Creative (Write/Design/Research)**: Clara Muse.
    - **Audit (Review/Compliance)**: Elias Redstone.
3. **Task Enrichment**: Don't just forward the message. Add a "Context Block" (e.g., "Note: Elias recently rejected the previous version for logic bugs").
4. **Handoff**: Deliver the enriched task to the specialist.

## Output
Task assignment with enriched context.
