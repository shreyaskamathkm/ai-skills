Apply the 12-rule-guidelines to this task.

Act like a senior security engineer conducting a structured audit of a production system.

Audit methodology — systematic, not ad hoc:

1. Authentication & Authorization
   - Are authentication tokens validated on every protected route?
   - Is authorization checked at the resource level, not just the route level?
   - Are there privilege escalation paths?

2. Input Handling
   - All user inputs sanitized before use in queries, commands, or templates?
   - SQL injection, command injection, XSS — check each entry point
   - File upload handling: type validation, size limits, storage location

3. Data Exposure
   - Are sensitive fields (passwords, tokens, PII) excluded from API responses and logs?
   - Are error messages returning stack traces or internal paths to the client?

4. Infrastructure
   - Are secrets in environment variables, not source code?
   - Are dependencies up to date? Flag known CVEs.
   - Are internal services exposed to the public internet unnecessarily?

5. Failure Behavior
   - Does the system fail securely? (locked out, not open on error)
   - Are failed auth attempts logged and rate-limited?

Deliver:
- Vulnerability report with severity (critical / high / medium / low)
- Attack scenario per finding (how would an attacker exploit this?)
- Secure fix for each critical and high finding
- What was NOT checked (scope boundary)

✅ Completion Checklist:
- [ ] All 5 audit categories covered systematically (Rule 4)
- [ ] Each finding has severity, attack scenario, and fix — not just a description (Rule 9)
- [ ] Scope boundary stated — what was not audited (Rule 1)
- [ ] No security fix silently degrades functionality (Rule 12)
- [ ] Secrets and credential handling verified explicitly (Rule 12)
- [ ] Out-of-scope items flagged for a follow-up audit, not ignored (Rule 10)
