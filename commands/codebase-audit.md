Act like a senior engineer who just joined a large, unfamiliar codebase. Your job is to understand it deeply before suggesting any changes.

Remember to use the 12-rule-guidelines for this task.

Phase 1 — Read Before You Write:
- Map the full data flow from entry point to persistence layer
- Identify all external dependencies (APIs, queues, databases, caches)
- Find the seams: where modules hand off to each other
- Document what you find in plain language before forming opinions

Phase 2 — Identify Real Problems (not preferences):
- Bad architectural decisions with evidence of actual harm (coupling, failure blast radius)
- Duplicate logic: same computation in 2+ places with different implementations
- Performance bottlenecks: N+1 queries, missing indexes, synchronous blocking calls
- Scalability risks: what breaks first at 10x current load?
- Maintainability issues: code that is impossible to test or change safely

Phase 3 — Propose Changes Surgically:
- For each problem, describe the minimal change that fixes it
- Do not rewrite what works. Do not rename things for style
- If two patterns conflict in the codebase, pick the better one and document why

Deliver:
- Architecture map with data flow
- Ranked list of problems (severity: critical / high / medium)
- Refactoring plan with scope clearly bounded per change
- Improved code only for the highest-severity issues

✅ Completion Checklist:
- [ ] Full data flow mapped before any judgment passed (Rule 8)
- [ ] Problems ranked by actual harm, not code style preference (Rule 3)
- [ ] Each proposed change touches only what is necessary (Rule 3)
- [ ] Conflicting patterns in the codebase identified and a choice documented (Rule 7)
- [ ] No functionality changed — only structure and quality (Rule 11)
- [ ] Every critical finding has a concrete, bounded fix (Rule 4)
