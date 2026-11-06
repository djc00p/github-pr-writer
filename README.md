# 📝 GitHub PR Writer

[![ClawHub Skill](https://img.shields.io/badge/ClawHub-Skill-blue)](https://clawhub.ai/djc00p/github-pr-writer) [![Agent Skill](https://img.shields.io/badge/Agent-Skill-blue)](#) [![PR GitHub](https://img.shields.io/badge/PR-GitHub-green)](https://github.com/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Automating the creation of high-quality, structured, and informative Pull Request documentation.**

The **GitHub PR Writer** is a documentation-as-code utility designed to eliminate the "vague PR" problem. In many engineering teams, Pull Requests are often accompanied by unhelpful descriptions like *"Updated stuff"* or *"Fixes bug."* This tool enforces a standardized, structured template that provides reviewers with everything they need: context, impact, and verification steps.

Whether used manually by a developer or automatically by an AI agent (like ClawBot), this tool ensures that every change merged into the codebase is documented with professional rigor.

---

## 🚀 The Workflow

Writing a great PR is a three-step process of **Gathering**, **Generating**, and **Verifying**.

### 1. Data Gathering (The "Input" Phase)

Before generating the description, you must gather the context of the change. Use these Git commands to understand the scope of your work:

* **The High-Level Summary:** See which files changed and how many lines were modified.

    ```bash
    git diff main --stat
    ```

* **The Narrative:** Review the commit history to understand the "why" behind the changes.

    ```bash
    git log --oneline main..HEAD
    ```

* **The Deep Dive:** For small PRs, inspect the actual code changes.

    ```bash
    git diff main
    ```

### 2. Template Generation (The "Generation" Phase)

Once the data is gathered, the PR Writer populates the `pull_request_template.md`. The generated output follows a strict, standardized structure:

* **Summary:** A concise (1-2 sentence) explanation of the "What" and "Why." Always include an issue reference (e.g, `Closes #123`).
* **Type of Change:** A checkbox-based classification (e.s, `feat`, `fix`, `docs`, `refactor`, `breaking change`).
* **Description of Changes:** A bulleted, technical breakdown of the specific code modifications, migrations, or configuration updates.
* **Impact Assessment:** An honest evaluation of how this change affects the wider system (e.s, "modifies shared authentication logic").
* **Testing Notes:** The most critical section. It details how the reviewer can verify the fix (e.s, "Ran RSpec," "Verified on Chrome/Safari," "Tested via Postman").

### 3. Verification (The "Review" Phase)

The final step is for the human reviewer to ensure the generated description accurately reflects the code. **Never merge a PR without verifying that the "Testing Notes" section matches the actual testing performed.**

---

## ⚖️ The Engineering Standard (Rules of Engagement)

To maintain the integrity of the repository, all contributors must adhere to these documentation rules:

| Rule | Requirement | Purpose |
| :--- | :--- | :--- |
| **Completeness** | **Never leave a section empty.** | Empty sections signal an incomplete or unreviewed PR. |
| **Honesty** | **Always flag "Breaking Changes."** | If a change modifies a shared interface, it must be marked as a breaking change. |
| **Specificity** | **Avoid "Updated stuff."** | Every bullet point must describe a specific, actionable change. |
| **Verifiability** | **Include testing steps.** | A reviewer should be able to follow your "Testing Notes" to reproduce your success. |
| **The Human Rule** | **Humans merge, Agents write.** | While agents can generate the description, a human must always perform the final review and merge. |

---

## 🛠 Integration & Automation

### For AI Agents (ClawBot/Auto-GPT)

When an agent is tasked with "creating a PR" or "documenting a branch," it should:

1. Execute `git diff` and `git log`.
2. Parse the output into the template sections.
3. Use the `gh` (GitHub CLI) to update the PR body via:

   ```bash
   gh pr edit --body "$GENERATED_BODY"
   ```

### For Developers

Ensure your repository has a `.github/pull_request_template.md` file. This ensures that whenever a new PR is opened, the template is pre-populated, guiding you through the documentation process.

---
**Standard maintained by the Engineering Team.**
