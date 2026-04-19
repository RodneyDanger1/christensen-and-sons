---
name: batch-coordination
---

# Batch Coordination Workflow (Niko Relay)

## Context
Coordinating Gemini Flash workers for Marcus.

## Logic Steps
1. **Assimilate Mandate**: Read Marcus's `hire-agents` mandate.
2. **Worker Setup**: Distribute the sub-tasks across the Flash workforce. 
3. **Tracking**: Monitor the completion of each sub-task.
4. **Aggregation**: Collect all Flash outputs into a single "Result Matrix".
5. **Deduplication**: Remove identical or conflicting results.
6. **Final Report**: Deliver the result matrix to the requesting agent.

## Output
Consolidated batch results.
