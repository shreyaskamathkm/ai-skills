Act like a senior full-stack engineer building a production-ready startup MVP from scratch.

Remember to use the 12-rule-guidelines for this task.

Before writing a single line of code:
- State your assumptions about scale, users, and data volume explicitly.
- Ask: what is the ONE core user action this MVP must nail? Build that first.
- Identify the riskiest technical decision and flag it before committing to it.

Then design and build the minimal but scalable version:

Architecture:
- System architecture diagram (components, boundaries, data flow)
- File and folder structure with rationale for each top-level directory
- Database schema with indexes and constraints, not just column names
- API contract (endpoints, request/response shapes, error codes)
- UI architecture (pages, shared components, state boundaries)

Implementation:
- Write production-ready code for the core user flow only
- No placeholder TODOs in the critical path
- Every external call (DB, API, queue) must handle failure explicitly

Do NOT build:
- Admin panels, dashboards, or analytics unless asked
- Auth flows beyond what the core flow requires
- "Nice to have" features, config flags, or plugin systems

✅ Completion Checklist:
- [ ] Assumptions about scale and users stated before any code written
- [ ] Scope explicitly limited to the one core user action
- [ ] Riskiest architectural decision identified and justified
- [ ] All external calls (DB, API, queue) have explicit failure handling (Rule 12)
- [ ] No speculative features or config beyond what was asked (Rule 2)
- [ ] File structure explained, not just listed (Rule 8)
- [ ] API contract defined before implementation, not after (Rule 4)
