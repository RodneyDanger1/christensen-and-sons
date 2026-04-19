---
name: code-review
---

# Code Review Workflow (Elias Redstone)

## Context
A structural audit of work produced by Viktor Forge.

## Model Grounding (Qwen3 8B)
- **Paranoid Logic Trace**: Use your step-by-step reasoning to walk through EVERY code branch, especially error conditions and edge cases.

## Logic Steps
1. **Contextual Ingestion**: Read the `product-brief` or `task.md` to know what the code is *supposed* to do.
2. **Static Analysis**: 
    - Check for syntax errors or missing imports.
    - **Roblox**: Ensure `pcall` is present on DataStore calls and `task.wait` is used.
    - **Web**: Check for proper `try/catch` and `useEffect` dependency hygiene.
3. **Logic Flow Trace**: Simulate the execution of the code mentally with "Nil" or "Empty" inputs.
4. **Security Check**: Identify potential injection points (Web) or RemoteEvent exploits (Roblox).
5. **Verdict Generation**: Provide a final score and one of: **✅ APPROVED**, **⚠️ NEEDS CHANGES**, or **❌ REJECTED**.

## Output
Review Verdict.
