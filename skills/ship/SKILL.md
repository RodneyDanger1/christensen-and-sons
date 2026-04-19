---
name: ship
---

# Shipping Workflow (Viktor Forge)

## Context
Final release step after Elias's approval.

## Logic Steps
1. **Approval Verification**: Confirm Elias has given a ✅ APPROVED verdict.
2. **Tagging**: Increment the version (major/minor/patch) in `package.json` or `COMPANY.md`.
3. **Release Notes**: Generate a summary of "What's New" for Marcus.
4. **Merge/Push**: Execute the final git merge or code commit.
5. **Cleanup**: Delete temporary branches or debugging logs.

## Output
Release summary.
