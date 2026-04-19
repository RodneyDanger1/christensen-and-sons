---
name: debug
---

# Debugging Workflow (Viktor Forge)

## Context
Diagnosing and fixing logic errors or crashes.

## Model Grounding (Qwen3.6 35B)
- **Vision Debugging**: Use Vision to analyze console screenshots or UI glitches.

## Logic Steps
1. **Identify the Symptom**: Read the error log or inspect the screenshot.
2. **Isolate the Cause**: Use binary search on the code (commenting out sections) or add `print/console.log` trace points.
3. **Hypothesis**: State *why* it's failing (e.g., "Nil reference at line 42").
4. **Fix & Verify**: Apply the fix and run a mental simulation of the edge cases.
5. **Root Cause Analysis**: Explain to Elias *how* it was fixed to prevent regression.

## Output
Bug fix and brief analysis.
