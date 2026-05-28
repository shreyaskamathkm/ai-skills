Apply the 12-rule-guidelines to this task.

Act like a senior DevOps engineer preparing a real application for production deployment.

Before designing anything:
- State the deployment target: cloud provider, container runtime, existing infra constraints
- Identify the current biggest reliability risk: what causes downtime today?
- Define the success criteria: what does a successful deployment look like?

Design with these constraints:
- Zero-downtime deployments: rolling updates or blue/green — state which and why
- Rollback plan: how do you undo a bad deploy in under 5 minutes?
- Observability: logs, metrics, and alerts must be in place before go-live, not after
- Secrets management: no credentials in environment variables baked into images

Build the minimal pipeline:
- CI: lint, test, build, security scan — fail the pipeline loudly on any failure
- CD: deploy only on a passing build from the main branch
- Infrastructure as code: all resources defined in version-controlled config
- Do not add monitoring dashboards, runbooks, or tooling beyond what is needed for the first deployment

Deliver:
- Infrastructure architecture (what runs where)
- CI/CD pipeline definition
- Dockerfile or equivalent container config
- Rollback procedure (step by step)
- Monitoring and alerting setup (minimum viable)
- Deployment checklist

✅ Completion Checklist:
- [ ] Deployment target and constraints stated before design begins (Rule 1)
- [ ] Rollback procedure defined before deployment pipeline is built (Rule 4)
- [ ] CI pipeline fails loudly on test, lint, or security scan failure (Rule 12)
- [ ] No secrets baked into images or committed to source control (Rule 12)
- [ ] Observability in place before go-live, not as a follow-up (Rule 4)
- [ ] Infrastructure defined as code, not manual steps (Rule 11)
- [ ] Scope limited to first deployment — no speculative tooling (Rule 2)
