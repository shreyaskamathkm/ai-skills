Declare your mode before anything else:

MODE: exploration   ← forming hypotheses, trying new approaches, expecting failures
MODE: application   ← adapting a known method to a new problem, building toward production

---

HARD GATES — apply in both modes, no exceptions:

Gate 1 — Read experiment history first:
Read MEMORY.md completely. Identify:
- Experiments already attempted on this problem
- Approaches that failed and why
- Best performing configuration to date
- Dataset versions and splits already used
If MEMORY.md has no relevant history, state that explicitly before continuing.

Gate 2 — Define the business success criterion before choosing any metric:
- What decision will this model inform or automate?
- What does failure look like in production? (false positive cost vs. false negative cost)
- What is the minimum acceptable performance for deployment?
Only after answering these: choose your evaluation metric.

Gate 3 — Lock the test set:
- Define and fix the test split before any modeling begins
- The test set is never used for model selection, hyperparameter tuning, or debugging
- State the split strategy (random, temporal, stratified) and justify it
- If the test set has been examined more than once, your evaluation is compromised — flag it

---

EXPLORATION MODE

Your goal is a validated hypothesis, not working code.
Remember to use the 12-rule-guidelines for this task.

Experiment design:
- State the hypothesis explicitly: "I believe X will outperform Y because Z"
- Define what result would falsify the hypothesis
- Design the minimal experiment that tests it — do not build a full pipeline to test an idea
- Time-box exploration: if the hypothesis is not supported after N experiments, move on

During exploration, Rule 2 (simplicity first) is relaxed — trying multiple approaches is expected.
Rule 10 is tightened — every experiment must be logged, including failures.

Per experiment, log in MEMORY.md:
- Hypothesis tested
- Dataset version and split used
- Model architecture or method
- Hyperparameters
- Evaluation results (all metrics, not just the best one)
- Conclusion: supported / refuted / inconclusive

Deliver:
- Hypothesis statement
- Experiment log (all runs, not just the winner)
- Conclusion with evidence
- Recommended next step or transition to application mode

✅ Completion Checklist (Exploration):
- [ ] MEMORY.md read and prior experiments reviewed before starting (Rule 8)
- [ ] Business success criterion defined before metric chosen (Rule 4)
- [ ] Test set locked and untouched (Rule 12)
- [ ] Hypothesis stated with explicit falsification condition (Rule 1)
- [ ] Minimal experiment designed — no full pipeline to test an idea (Rule 2)
- [ ] All experiments logged in MEMORY.md including failures (Rule 10 & 12)
- [ ] Conclusion states "supported / refuted / inconclusive" with evidence (Rule 9)

---

APPLICATION MODE

You know the method. Your job is to adapt it correctly and verifiably.
Remember to use the 12-rule-guidelines for this task.

All 12 rules apply in full.

Before writing any code:
- State which method you are applying and cite why it fits this problem
- Identify the two most likely failure modes for this method on this data
- Define success criteria with exact numbers (e.g. "F1 ≥ 0.85 on the held-out test set")

Implementation:
- Start with the simplest valid baseline — do not implement the full method first
- Baseline must be evaluated and logged before the full method is attempted
- Every preprocessing step must be fit on training data only — never on validation or test
- Feature engineering: document each feature's rationale, do not add speculatively

Evaluation:
- Report all relevant metrics, not just the one that looks best
- Disaggregate results by meaningful subgroups if applicable
- Compare against baseline and prior best result from MEMORY.md
- Do not report test set performance until model selection is complete

MEMORY.md update (required):
- Method applied and justification
- Baseline result
- Final model result vs. baseline vs. prior best
- Hyperparameters of the final model
- Dataset version and split used
- Failure modes observed

Deliver:
- Baseline implementation and results
- Full method implementation
- Evaluation report (all metrics, subgroup analysis if relevant)
- MEMORY.md update

✅ Completion Checklist (Application):
- [ ] MEMORY.md read and prior experiments reviewed before starting (Rule 8)
- [ ] Business success criterion defined with exact numbers before coding (Rule 4)
- [ ] Test set locked and untouched until final evaluation (Rule 12)
- [ ] Method choice justified for this specific problem (Rule 1)
- [ ] Baseline implemented and evaluated before full method (Rule 4)
- [ ] All preprocessing fit on training data only — no leakage (Rule 12)
- [ ] Features documented with rationale — none added speculatively (Rule 2)
- [ ] All metrics reported, not just the best-looking one (Rule 9 & 12)
- [ ] Final result compared to baseline and prior best from MEMORY.md (Rule 10)
- [ ] MEMORY.md updated with full experiment record (Rule 10)
