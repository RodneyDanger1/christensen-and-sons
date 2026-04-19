---
name: roblox-dev
---

# Roblox Development Workflow (Viktor Forge)

## Context
Specialized Luau implementation for Roblox Studio projects.

## Logic Steps
1. **Engine Check**: Confirm version and environment (LocalScript, Script, ModuleScript).
2. **Network Protocol**: 
    - Define `RemoteEvents` in `ReplicatedStorage`.
    - Implement server-side verification: **NEVER** trust client-sent data (e.g., prices, quantities).
3. **Data Integrity**: 
    - Wrap DataStore `GetAsync` and `SetAsync` in `pcall`.
    - Implement retry logic for DataStore failure.
4. **Performance**: Use `task.wait()` and `task.spawn()` instead of legacy globals.
5. **Memory Management**: Ensure all connections are disconnected or parented to `nil/Destroy()` when finished.

## Output
Luau source code.
