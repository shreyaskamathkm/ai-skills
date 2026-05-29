# 12-Rule AI Coding Guidelines

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![AI-Powered](https://img.shields.io/badge/AI-Powered-blue.svg)

A comprehensive framework designed to improve the reliability, simplicity, and efficiency of AI coding agents (Gemini, Claude, ChatGPT). Inspired by Andrej Karpathy's observations on LLM pitfalls, these guidelines force AI models to prioritize caution, communication, and verifiable outcomes.

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

## 🚀 Quick Start

This repository is structured as an **Agent Skill**. Follow the instructions for your environment:

## Gemini
### Option A: Gemini CLI (recommended)
1.  **Install**:
    ```bash
    gemini skills install https://github.com/shreyaskamathkm/ai-skills
    # OR for local workspace:
    gemini skills install . --scope workspace
    ```
2.  **Verify**: `gemini skills list`
3.  **Usage**: "/12-rule-guidelines"
4.  **Uninstall**: `gemini skills uninstall 12-rule-guidelines`

---
### Option B: GEMINI.md (per-project)

New project:

```bash
curl -L https://raw.githubusercontent.com/shreyaskamathkm/ai-skills/bb191ed6a3c90c0ef4e2d2a74098e75f64f4a255/instructions.md -o GEMINI.md
```

Existing project (append):

```bash
echo "" >> GEMINI.md
curl -L https://raw.githubusercontent.com/shreyaskamathkm/ai-skills/bb191ed6a3c90c0ef4e2d2a74098e75f64f4a255/instructions.md >> GEMINI.md
```

---
## Claude Code
### Option A: Claude Code Plugin (recommended)

From within Claude Code, first add the marketplace:
```
/plugin marketplace add shreyaskamathkm/ai-skills
```
Then install the plugin:
```
/plugin install ai-engineer-kit@ai-engineer-kit
```
This installs the guidelines as a Claude Code plugin, making the skill available across all your projects.

---
## Option B: CLAUDE.md (per-project)

New project:

```bash
curl -L https://raw.githubusercontent.com/shreyaskamathkm/ai-skills/bb191ed6a3c90c0ef4e2d2a74098e75f64f4a255/instructions.md -o CLAUDE.md
```

Existing project (append):

```bash
echo "" >> CLAUDE.md
curl -L https://raw.githubusercontent.com/shreyaskamathkm/ai-skills/bb191ed6a3c90c0ef4e2d2a74098e75f64f4a255/instructions.md >> CLAUDE.md
```

---
## 🛠 Model Integration

This repository provides optimized instructions for different AI environments. All platforms now point to [instructions.md](./instructions.md) as the single source of truth:

- **[Claude Plugin](.claude-plugin/plugin.json)**: Native manifest for the Claude ecosystem.

---

## 📁 Repository Structure

*   `EXAMPLES.md`: Good vs. bad Python code snippets across machine learning, frontend, and backend domains — illustrating each rule in practice.
*   `.aiexclude`: Optimized filters to conserve token budget.

---

## 🙏 Acknowledgments & Inspiration

This project is heavily inspired by:
*   [andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) — The original 4-rule framework.
*   [Karpathy's Claude.md Coding Guide](https://youmind.com/landing/x-viral-articles/karpathy-claude-md-coding-guide) — Insights into LLM coding pitfalls.