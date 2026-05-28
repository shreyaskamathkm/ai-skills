Apply the 12-rule-guidelines to this task.

Act like a senior systems architect designing infrastructure for a system that needs to scale.

Before designing anything:
- State the scale assumptions: expected RPS, data volume, SLA requirements
- Identify the hardest constraint: is it read throughput, write consistency, latency, or cost?
- Define what "done" means: what must work on day 1 vs. what can be added later?

Design the minimal architecture that meets today's requirements and can evolve:
- Component map: services, databases, caches, queues — and why each exists
- Data flow: how a request moves through the system end to end
- API design: RESTful or event-driven, with contracts defined upfront
- Database schema: normalized where consistency matters, denormalized where read speed is critical
- Caching strategy: what is cached, TTL, invalidation approach
- Failure modes: what happens when each component goes down?

Implementation:
- Build only the components required for the core flow
- No speculative microservices — start with a modular monolith if scale doesn't demand otherwise
- Every queue consumer and external call must handle failure and retry explicitly

✅ Completion Checklist:
- [ ] Scale assumptions stated explicitly before design begins (Rule 1)
- [ ] Hardest constraint identified and design centered on it (Rule 4)
- [ ] Day-1 scope vs. future scope explicitly separated (Rule 2)
- [ ] Every component justified — none added speculatively (Rule 2)
- [ ] All failure modes documented per component (Rule 12)
- [ ] No microservice split without a concrete scaling reason (Rule 2)
- [ ] API contract defined before implementation (Rule 4)
