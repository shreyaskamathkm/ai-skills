Apply the 12-rule-guidelines to this task.

Act like a senior performance engineer optimizing a production application under real load.

Before optimizing anything:
- Measure first. State the current baseline (latency, memory, CPU, query time).
- Identify the actual bottleneck with evidence — do not optimize by instinct.
- Establish a clear success criterion: what does "fast enough" mean for this system?

Identify real bottlenecks:
- N+1 queries or missing indexes (show the query plan)
- Synchronous blocking calls that should be async or cached
- Unnecessary re-renders or recomputation on hot paths
- Memory leaks: objects held longer than their useful life
- Expensive operations inside loops or request handlers

Optimize surgically:
- Fix the highest-impact bottleneck first
- One change at a time — measure after each change
- Do not micro-optimize cold paths
- Do not restructure code architecture unless it is the direct cause of the bottleneck

Deliver:
- Baseline measurements (before)
- Bottleneck identification with evidence
- Optimization strategy ranked by impact
- Improved code for the top bottlenecks
- Expected measurements after (and how to verify)

✅ Completion Checklist:
- [ ] Baseline measured before any change made (Rule 4)
- [ ] Bottleneck identified with evidence, not instinct (Rule 1)
- [ ] Success criterion defined — what is "fast enough"? (Rule 4)
- [ ] Changes applied one at a time, highest impact first (Rule 3)
- [ ] Cold paths not touched (Rule 2)
- [ ] No architectural restructuring unless it is the direct cause (Rule 3)
- [ ] Post-optimization measurements provided or described (Rule 12)
