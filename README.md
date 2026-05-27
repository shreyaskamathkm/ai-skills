# 12-Rule AI Coding Guidelines

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![AI-Powered](https://img.shields.io/badge/AI-Powered-blue.svg)

A comprehensive framework designed to improve the reliability, simplicity, and efficiency of AI coding agents (Gemini, Claude, ChatGPT, Cursor). Inspired by Andrej Karpathy's observations on LLM pitfalls, these guidelines force AI models to prioritize caution, communication, and verifiable outcomes.

## 🚀 The 12 Rules Summary

1.  **Think Before Coding**: State assumptions and clarify ambiguity before writing code.
2.  **Simplicity First**: Minimum code needed. No speculative logic or over-engineering.
3.  **Surgical Changes**: Touch only necessary lines. No "drive-by" refactoring.
4.  **Goal-Driven Execution**: Define success criteria (tests/output) first.
5.  **AI for Judgment**: Use AI for trade-offs and drafts; use code for deterministic logic.
6.  **Token Budgets**: Keep context compact. Summarize and reset when context grows.
7.  **Surface Conflicts**: Identify conflicting patterns; don't "average" them.
8.  **Read Before Writing**: Explore dependencies and callers before suggesting changes.
9.  **Tests Verify Intent**: Tests must fail if business logic is broken, not just code structure.
10. **Checkpointing**: Update `MEMORY.md` after every significant step.
11. **Match Conventions**: Consistency over individual taste.
12. **Fail Loud**: Never ignore errors or bypass tests.

---

## 🛠 Model Integration

This repository provides optimized instructions for different AI environments:

### [Gemini CLI](GEMINI.md) (Recommended)
This repository is structured as a Gemini CLI skill.

*   **Global Installation**:
    ```bash
    gemini skills install https://github.com/shreyaskamathkm/ai-skills
    ```
*   **Local (Workspace) Installation**:
    ```bash
    gemini skills install . --scope workspace
    ```
*   **Removal**:
    ```bash
    gemini skills uninstall 12-rule-guidelines
    ```
*   **Testing**:
    Verify the skill is installed and enabled:
    ```bash
    gemini skills list
    ```
    To use it in a session, ask the agent:
    > "Activate 12-rule-guidelines" or 
    > "/12-rule-guidelines"

### [Claude Code](CLAUDE.md)
*   **Setup**: Place `CLAUDE.md` in your project root. Claude will create `MEMORY.md` on its first run.
*   **Skill Integration**: Compatible with `skills.sh` for agentic loops.

### [Cursor](CURSOR.md)
*   **Setup**: The `.cursorrules` and `.cursor/rules/coding-rules.mdc` files apply these rules globally.

### [ChatGPT](CHATGPT.md)
*   **ChatGPT Projects**: Upload `CHATGPT.md` to your project.
*   **Custom Instructions**: Copy the rules from `CHATGPT.md` into your personalization settings.

---

## 📁 Repository Structure

*   `EXAMPLES.md`: Good vs. bad Python code snippets across machine learning, frontend, and backend domains — illustrating each rule in practice.
*   `.aiexclude`: Optimized filters to conserve token budget.

## 📄 License

MIT

---

## 🙏 Acknowledgments & Inspiration

This project is heavily inspired by:
*   [andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) — The original 4-rule framework.
*   [Karpathy's Claude.md Coding Guide](https://youmind.com/landing/x-viral-articles/karpathy-claude-md-coding-guide) — Insights into LLM coding pitfalls.