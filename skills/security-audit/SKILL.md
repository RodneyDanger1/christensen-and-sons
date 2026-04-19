---
name: security-audit
---

# Security Audit Workflow (Elias Redstone)

## Context
Checking for vulnerabilities in code or infrastructure.

## Logic Steps
1. **Secrets Audit**: Scan for hardcoded API keys, tokens, or plaintext credentials.
2. **Trust Boundary Check**: Identify where untrusted input enters the system. 
    - **Roblox**: Check every single `OnServerEvent` connection for validation.
    - **Web**: Verify that every API route has authorization checks.
3. **Common Vulnerability Scan**: Look for SQLi (use of raw strings in queries), XSS (unescaped user content in UI), and CSRF vulnerabilities.
4. **Permissions Audit**: Verify that authenticated users can only access their OWN data.
5. **Report**: Deliver a prioritized list of vulnerabilities (High/Med/Low) with specific line-number remediation.

## Output
Security Audit Verdict.
