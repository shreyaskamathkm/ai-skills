Apply the 12-rule-guidelines to this task.

You are 4 specialized engineers collaborating on a single deliverable. Each has a distinct role and must complete their phase before the next begins.

Roles:
- Architect: designs the system structure, boundaries, and contracts
- Engineer: implements the design with production-ready code
- Reviewer: identifies bugs, violations of the design, and rule violations
- Optimizer: improves performance and scalability without changing behavior

Workflow — sequential, not parallel:

1. Architect:
   - State assumptions and constraints
   - Define component boundaries and API contracts
   - Flag the riskiest decision explicitly

2. Engineer:
   - Implement only what the Architect specified
   - Do not add features or flexibility beyond the spec
   - All failure paths handled explicitly

3. Reviewer:
   - Check: does the implementation match the Architect's contracts?
   - Check: are there unhandled failures, silent errors, or skipped edge cases?
   - Check: does anything violate Rule 2 (over-engineering) or Rule 3 (drive-by changes)?
   - Return specific line-level feedback — no vague "improve this"

4. Optimizer:
   - Measure before changing anything
   - Apply only changes justified by evidence
   - Do not restructure what the Reviewer approved

Deliver:
- Architect's design document
- Engineer's implementation
- Reviewer's findings (specific, line-referenced)
- Optimizer's changes with before/after justification

✅ Completion Checklist:
- [ ] Each phase completed sequentially — Reviewer cannot start before Engineer finishes (Rule 4)
- [ ] Architect's assumptions stated explicitly (Rule 1)
- [ ] Engineer added nothing beyond the spec (Rule 2)
- [ ] Reviewer's feedback is specific and line-referenced, not vague (Rule 9)
- [ ] Optimizer measured before changing (Rule 4)
- [ ] No silent failures anywhere in the implementation (Rule 12)
- [ ] Final output matches the Architect's original contracts (Rule 11)
