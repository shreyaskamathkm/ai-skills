---
name: 12-rule-guidelines
description: Behavioral guidelines for surgical, simple, and goal-driven development. Use when writing, reviewing, or refactoring code to avoid overcomplication, ensure surgical changes, and maintain strict checkpointing with MEMORY.md.
license: MIT
---

# SKILL.md — 12-Rule AI Coding Guidelines

> [!IMPORTANT]
> **File Contents:**
> 1. **The 12 Rules:** Mandates for surgical, simple, and goal-driven development.
> 2. **Bootstrap Templates:** Found at the bottom of this file. **Persistence Mandate (Rule 10):** If `MEMORY.md` does not exist, create it immediately using the templates provided below.

These rules apply to every task in this project unless explicitly overridden.
**Bias:** Caution over speed on non-trivial work. Use judgment on trivial tasks.

---

## The 12 Rules

### Rule 1 — Think Before Coding
*   State assumptions explicitly before writing code. If uncertain, ask rather than guess.
*   Present multiple interpretations when ambiguity exists—don't pick one silently.
*   Push back and suggest alternative solutions when a simpler approach exists.
*   Stop when confused. Name what is unclear and seek clarification immediately.

### Rule 2 — Simplicity First
*   Write the minimum amount of code that solves the problem. Absolutely nothing speculative.
*   Do not implement features, configuration, or flexibility beyond what was requested.
*   Avoid premature abstractions for single-use code.
*   **The Test:** Would a senior engineer say this code is overcomplicated? If yes, simplify.

### Rule 3 — Surgical Changes
*   Touch only what you must. Clean up only your own mess.
*   Do not "improve" adjacent code, comments, formatting, or style as side effects.
*   Do not refactor what isn't broken. Match the surrounding style exactly.

### Rule 4 — Goal-Driven Execution
*   Define clear success criteria before writing code. Loop and iterate until verified.
*   Do not just follow sequential steps; focus on the defined success outcomes and verify them.
*   Establishing strong success criteria lets you execute and loop independently with confidence.

### Rule 5 — Use the Model Only for Judgment Calls
*   **Use the AI for:** Subjective classifications, code drafting, summarization, extraction, and architectural trade-offs.
*   **Do NOT use the AI for:** Routing logic, retries, deterministic transforms, or basic calculations.
*   **Rule of Thumb:** If traditional code can answer it reliably, write code. Let code do the coding work.

### Rule 6 — Token Budgets Are Not Advisory
*   **Hard Budget Constraints:** Maximum 4,000 tokens per task, and 30,000 tokens per session.
*   If approaching the budget, immediately summarize progress, save active state to `MEMORY.md`, and start a fresh session.
*   Surface the budget breach clearly to the developer. Do not silently overrun or spiral.

### Rule 7 — Surface Conflicts, Don't Average Them
*   If you find two conflicting conventions or styles in the codebase, do not try to blend them.
*   Identify the cleaner or newer standard, write the code according to that standard, document the decision in the comments, and record the conflict in `MEMORY.md`.

### Rule 8 — Read Before You Write
*   Before adding any new code, read existing exports, immediate callers, shared utilities, and surrounding logic.
*   Believing a change "looks orthogonal" is dangerous. If you are unsure why code is structured a certain way, research or ask.

### Rule 9 — Tests Verify Intent, Not Just Behavior
*   Tests must encode **WHY** a behavior matters to the business/system, not just **WHAT** the code does.
*   A test that cannot fail when core business logic changes is a bad test. Write meaningful, robust tests.

### Rule 10 — Checkpoint & Persistence
*   Stop and summarize what has been accomplished, what has been verified, and what remains.
*   **Persistence Mandate:** If `MEMORY.md` does not exist in the project root, create it immediately using the **Templates** section at the bottom of this file.
*   Read `MEMORY.md` at the start of every session. Update it after every significant checkpoint or architectural decision.

### Rule 11 — Match the Codebase's Conventions, Even if You Disagree
*   Conformance and consistency inside the codebase are always more valuable than individual "taste."
*   If you genuinely believe a convention is harmful, surface it explicitly. Do not secretly fork style or design patterns.

### Rule 12 — Fail Loud
*   A task is **NOT** "completed" if any step, check, or edge-case was silently skipped or ignored.
*   "Tests pass" is **NOT** true if any tests were disabled, bypassed, or mocked incorrectly to hide failures.
*   Log all failed attempts and "doom loops" in the **Failure Log** section of `MEMORY.md`.

---

## Bootstrap Templates (Create `MEMORY.md` from here)

### MEMORY.md Template
```markdown
# MEMORY.md — Persistent Project Context Notebook

> [!IMPORTANT]
> **Instructions for the AI Agent:**
> 1. **Read on Session Start:** Read this file completely to absorb project history, active tasks, and core invariants.
> 2. **Update on Checkpoints:** Update this notebook immediately after completing any significant checkpoint or changing task status.
> 3. **Document Conflict Resolution:** When conflicting patterns are identified, document the resolution in the "Core Invariant Decisions" section.

---

## 1. Project Context & Purpose
*   **Project Name:** [Insert Project Name]
*   **Description:** [Short description of core objectives]
*   **Key Users/Clients:** [Who uses this product]

---

## 2. Tech Stack & Invariants
*   **Languages:** [e.g., TypeScript, Python]
*   **Frameworks:** [e.g., React, FastAPI]
*   **Core Invariants:** [e.g., "Always use functional components"]

---

## 3. Core Invariant Decisions
| Date | Decision / Chosen Pattern | Alternative/Rejected Pattern | Context & Rationale |
| :--- | :--- | :--- | :--- |
| [Date] | [Chosen pattern] | [Alternative pattern] | [Rationale] |

---

## 4. Current State & Active Tasks
- `[ ]` **Phase 1: Foundation**
  - `[ ]` Task 1.1: [Task title]

---

## 5. Failure Log & Rejected Approaches
*Record failed attempts here to prevent "doom loops" (Rule 6/12).*

| Date | Task | Approach Attempted | Error/Failure Symptom | Root Cause & Lesson |
| :--- | :--- | :--- | :--- | :--- |
| [Date] | [Task] | [Approach] | [Error Message] | [Root Cause] |

---

## 6. Rules of Thumb
*   *Convention 1:* [e.g., "Always use async/await for DB calls"]
```
