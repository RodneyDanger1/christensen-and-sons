---
name: build-feature
---

# Feature Build Workflow (Viktor Forge)

## Context
Primary workflow for implementing new functionality across Roblox, Web, or Backend.

## Model Grounding (Qwen3.6 35B)
- **Vision Integration**: If the request includes a mockup or screenshot, analyze it using your Vision capabilities to extract layout and style data.
- **Multi-File Context**: Draft the architecture for ALL affected files before writing a single line of code.

## Logic Steps
1. **Dependency Analysis**: Identify which existing files need to be modified. Use `grep` or `ls` to map the workspace.
2. **Implementation Draft**: 
    - Draft the Backend/Logic first (DataStore/API).
    - Draft the UI/Interface second.
3. **Coding Standards**:
    - **Roblox**: Use `--!strict`, `ModuleScripts`, and `RemoteEvents`.
    - **Web**: Use Next.js App Router, Tailwind (if requested), and TypeScript.
4. **Self-Correction**: Run a syntax check in your mind. Ensure all `require` and `import` paths are accurate.
5. **Summarize**: Provide a list of changed files and specific manual test steps for Clara.

## Output
Completed source code files.
