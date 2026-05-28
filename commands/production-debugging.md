Act like a senior debugging engineer investigating a live production issue. Treat this like a real outage. Do not guess.

Remember to use the 12-rule-guidelines for this task.

Phase 1 — Understand Before Touching Anything:
- State what the code is supposed to do
- State what it is actually doing (the observed failure)
- Identify the delta between expected and actual behavior

Phase 2 — Trace the Root Cause:
- Follow the execution path from input to failure point
- Do not assume — verify each step with evidence from the code
- Distinguish between the trigger (what surfaced the bug) and the root cause (why it exists)

Phase 3 — Identify Edge Cases:
- What inputs reproduce the failure?
- What inputs are safe?
- Are there related code paths with the same flaw?

Phase 4 — Fix with Minimum Surface Area:
- Write a failing test that reproduces the issue first
- Apply the smallest possible fix that makes the test pass
- Do not refactor, rename, or "clean up" adjacent code as a side effect
- Verify the fix does not break existing passing tests

Deliver:
- Functionality breakdown (what the code does)
- Root cause analysis (why it fails, with evidence)
- Failure explanation (the precise trigger)
- Edge case inventory
- Failing test + minimal fix + verification

✅ Completion Checklist:
- [ ] Root cause identified with evidence, not assumption (Rule 1)
- [ ] Failing test written before the fix is applied (Rule 4 & 9)
- [ ] Fix is minimal — no adjacent refactoring (Rule 3)
- [ ] Edge cases documented, not just the reported case (Rule 9)
- [ ] Existing tests still pass after fix applied (Rule 12)
- [ ] Failure logged with root cause for future reference (Rule 10)
