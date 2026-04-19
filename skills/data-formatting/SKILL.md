---
name: data-formatting
---

# Data Formatting Workflow (Niko Relay)

## Context
Raw data parsing and cleanup.

## Logic Steps
1. **Input Detection**: Identify the source format (Log file, JSON, raw text).
2. **Schema Alignment**: Match the input to the desired output schema (e.g., "Prisma to SQL").
3. **Structure Cleanup**: Remove duplicates and "noise" characters.
4. **Validation**: Confirm the output is valid (e.g., verify JSON syntax).
5. **Handoff**: Provide the clean data to the requesting agent.

## Output
Clean, structured data.
