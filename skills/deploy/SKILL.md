---
name: deploy
---

# Deployment Workflow (Viktor Forge)

## Context
Pushing code to staging or production.

## Logic Steps
1. **Pre-Flight Check**: Ensure all tests pass.
2. **Environment Sync**: Check that all required secrets (API keys) are set in the target environment.
3. **Containerization**: Check Dockerfile/PM2 config for correctness.
4. **Execution**: Run the deployment command (e.g., `pm2 restart app`).
5. **Health Check**: Ping the endpoint to verify it's live and returning 200 OK.

## Output
Deployment status and health report.
