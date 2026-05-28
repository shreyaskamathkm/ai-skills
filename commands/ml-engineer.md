Read MEMORY.md before starting. Identify:
- Current model in production (version, performance, deployment date)
- Known pipeline issues or technical debt
- Prior serving architecture decisions and their rationale
- Any drift alerts or monitoring gaps flagged previously

State which phase you are entering:

PHASE 1: Training Pipeline
PHASE 2: Model Serving

Phase 2 cannot begin until the Phase 1 gate is explicitly cleared.

---

PHASE 1 — Training Pipeline
Remember to use the 12-rule-guidelines for this task.

Goal: a reproducible, validated, tracked pipeline that produces a reliable model artifact.

Before writing any pipeline code:
- State the data sources, versions, and access method
- Identify the highest data quality risk: what could corrupt training silently?
- Define "pipeline success": what must be true for a training run to be considered valid?

Data validation (required before training starts):
- Schema validation: expected columns, types, and value ranges enforced
- Distribution checks: flag significant drift from the training distribution used in prior runs
- Leakage check: verify no target-correlated features derived from the future
- If validation fails, the pipeline must stop loudly — no silent bad training runs (Rule 12)

Reproducibility requirements:
- Random seeds set and logged for all stochastic operations
- Dataset version pinned — not "latest"
- Dependency versions pinned in requirements or lockfile
- Same code + same data + same seed must produce the same model artifact

Experiment tracking (wired in from run 1, not added later):
- Every run logs: dataset version, hyperparameters, metrics, artifact location
- Failed runs logged with failure reason — not silently discarded
- Comparison against baseline and prior best automatic, not manual

Pipeline failure behavior:
- Data validation failure → stop, log reason, do not proceed to training
- Training divergence → stop, log hyperparameters and loss curve, do not save artifact
- Metric below threshold → flag, log, do not promote artifact to serving

MEMORY.md update after Phase 1:
- Pipeline version and changes made
- Dataset version used
- Training run results (all metrics)
- Model artifact location and checksum
- Known limitations or data quality issues observed

Phase 1 Gate — all of the following must be true before Phase 2 begins:
- [ ] Pipeline produces identical output given same inputs (reproducibility verified)
- [ ] Data validation runs and fails loudly on bad data
- [ ] All runs tracked with full metadata
- [ ] Model artifact is versioned and checksummed
- [ ] MEMORY.md updated with Phase 1 results

---

PHASE 2 — Model Serving

Goal: serve the model artifact reliably, observably, and with a tested rollback path.
Remember to use the 12-rule-guidelines for this task.

Before designing serving architecture:
- State latency requirement (p50, p99) and throughput requirement (requests/sec)
- State the current model in production — this is what you are replacing
- Define the rollback trigger: what metric or condition initiates a rollback?
- Identify the failure mode that is hardest to detect: silent prediction degradation

Serving architecture:
- Choose the minimal serving approach that meets the latency/throughput requirement
- Do not add a feature store, model registry, or caching layer unless required by the constraint
- Batch vs. real-time: state which and justify — do not default to real-time

Deployment strategy:
- Shadow mode first: new model runs alongside production, predictions logged but not served
- Canary second: new model serves a small percentage of traffic with metrics compared
- Full cutover only after canary metrics match or exceed production for a defined period
- Rollback procedure: step-by-step, executable in under 5 minutes, tested before go-live

Monitoring (required before go-live, not after):
- Input data drift: distribution of incoming features vs. training distribution
- Prediction drift: distribution of model outputs over time
- Latency: p50, p99 tracked and alerted on breach
- Error rate: prediction failures, timeout rate
- Business metric: the metric that actually matters, not just model metrics

Silent degradation is treated as seriously as a crash. An unmonitored model in production is a Rule 12 violation.

MEMORY.md update after Phase 2:
- Serving architecture chosen and rationale
- Deployment strategy used
- Monitoring setup and alert thresholds
- Rollback procedure (link or inline)
- Canary results before full cutover
- Known serving limitations

Deliver:
- Serving architecture design
- Deployment plan (shadow → canary → cutover)
- Rollback procedure (step by step)
- Monitoring and alerting setup
- MEMORY.md update

✅ Completion Checklist (Phase 1 — Training Pipeline):
- [ ] MEMORY.md read before starting (Rule 8)
- [ ] Data validation runs before training and fails loudly on bad data (Rule 12)
- [ ] Leakage check performed explicitly (Rule 12)
- [ ] Reproducibility verified: same inputs produce same artifact (Rule 4)
- [ ] All runs tracked including failures (Rule 10 & 12)
- [ ] Pipeline stops loudly on divergence or metric threshold breach (Rule 12)
- [ ] Model artifact versioned and checksummed (Rule 10)
- [ ] MEMORY.md updated with full Phase 1 record (Rule 10)

✅ Completion Checklist (Phase 2 — Model Serving):
- [ ] Phase 1 gate explicitly cleared before Phase 2 begins (Rule 4)
- [ ] Latency and throughput requirements stated before architecture chosen (Rule 1)
- [ ] Rollback procedure defined and tested before go-live (Rule 4 & 12)
- [ ] Shadow mode run before canary deployment (Rule 4)
- [ ] Monitoring live before full cutover — not added later (Rule 12)
- [ ] Silent prediction degradation covered by monitoring (Rule 12)
- [ ] Serving architecture minimal for the stated requirements (Rule 2)
- [ ] MEMORY.md updated with full Phase 2 record (Rule 10)
