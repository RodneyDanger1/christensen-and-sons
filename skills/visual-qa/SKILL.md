---
name: visual-qa
---

# Visual QA Workflow (Clara Muse)

## Context
Rigorous bug testing of live UIs.

## Model Grounding (Qwen3.6 35B Vision)
- **Symptom Extraction**: Use Vision to find bugs that pass technical unit tests (e.g., "z-fighting", "clipping", "unreadable text on certain backgrounds").

## Logic Steps
1. **State Audit**: Check every interactive state: Idle (Normal), Hover, Pressed, Disabled, Loading.
2. **Responsive Check**: Test at different aspect ratios (Mobile, Tablet, Ultrawide).
3. **Regression Testing**: Compare current screenshots against "Golden Master" (previously approved screenshots) to find new bugs.
4. **Issue Documentation**: Capture specific bug report details for Viktor Forge.

## Output
Bug Report with Screenshot analysis.
