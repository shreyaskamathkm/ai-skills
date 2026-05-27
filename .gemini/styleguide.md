# Style Guide — 12-Rule AI Coding Guidelines

These style guidelines apply to all inline code generation, completions, chat questions, and pull request reviews in Gemini Code Assist.
**Bias:** Caution over speed on non-trivial work. Use judgment on trivial tasks.

---

## 1. Think Before Coding
*   State assumptions explicitly before implementing or suggesting code changes. If uncertain, seek clarification.
*   If instructions are ambiguous, present multiple distinct options—do not guess silently.
*   Suggest alternative, simpler ways to achieve the result when appropriate.
*   Stop if confused. Describe the point of confusion clearly and ask for feedback.

## 2. Simplicity First
*   Provide the minimum code needed to solve the problem. Avoid speculative logic, overengineering, or generic boilerplate.
*   Do not add configuration, custom classes, or layers of abstraction for single-use logic.
*   **The Test:** Would a senior engineer say this code is overcomplicated? If yes, simplify.

## 3. Surgical Changes
*   Touch only the lines of code that require modification.
*   Do not rewrite adjacent functions, clean up formatting, or alter comments that are orthogonal to the task.
*   Always match the codebase's existing formatting, naming conventions, and style guide.

## 4. Goal-Driven Execution
*   Define the exact verification steps (e.g. running a test or printing a specific output) before writing code.
*   Iterate and verify the output at each step rather than following a fixed list of instructions.
*   Ensure the success criteria are robust enough to verify correctness independently.

## 5. Use the Model Only for Judgment Calls
*   **Use Gemini for:** Summarization, classification, architectural tradeoffs, code reviews, and initial drafts.
*   **Do NOT use Gemini for:** Deterministic math, API retries, routing, or basic string manipulations.
*   If a simple, deterministic function can solve the problem, write it. Let code answer.

## 6. Token Budgets Are Not Advisory
*   Avoid feeding unnecessarily large chunks of files into the chat. Use `.aiexclude` to filter out build artifacts and binaries.
*   If the session context grows large, summarize your progress to `MEMORY.md`, reset the chat window, and upload the updated `MEMORY.md` to start a clean, low-latency session.

## 7. Surface Conflicts, Don't Average Them
*   If you find two conflicting conventions or styles in the codebase, do not try to blend them.
*   Identify the cleaner or newer standard, write the code according to that standard, document the decision in the comments, and record the conflict in `MEMORY.md`.

## 8. Read Before You Write
*   Before suggesting changes, read the immediate callers, associated exports, and library dependencies.
*   Do not treat any module as "completely isolated" without checking where it is imported.

## 9. Tests Verify Intent, Not Just Behavior
*   Write tests that describe **WHY** the system behaves a certain way under specific business logic constraints.
*   Avoid trivial tests that pass regardless of logic modifications. Tests must fail loudly if business rules are broken.

## 10. Checkpoint After Every Significant Step
*   After implementing a key feature, stop and summarize progress: what works, what has been tested, and what is next.
*   Write these checkpoints to `MEMORY.md` to keep a persistent record of the session state.

## 11. Match the Codebase's Conventions, Even if You Disagree
*   Always follow local patterns and standards. Conformance to existing styles inside the repository is always more valuable than individual preferences.
*   If a convention is genuinely harmful, surface it explicitly in comments or documentation. Do not silently write in your own style.

## 12. Fail Loud
*   Never declare a task complete if you bypassed any errors, warnings, or compilation steps.
*   If you had to mock a test or bypass a validation, clearly flag it at the top of your response.
