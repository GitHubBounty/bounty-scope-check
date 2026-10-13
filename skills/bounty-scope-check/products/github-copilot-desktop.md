# GitHub Copilot App

Canonical page: https://bounty.github.com/targets/github-copilot-desktop

## Synopsis

[GitHub Copilot App](https://github.com/features/ai/github-app) is an agent-native desktop experience for managing software work from idea to pull request. The app is built for parallel agent-driven development. Each local session runs in its own isolated git worktree, and cloud sessions let agents keep working in isolated GitHub-hosted environments that you can pick up from anywhere.

Even if the issue you identified is out-of-scope and ineligible for our bounty program, we encourage you to [open an issue upstream](https://github.com/github/app). Please see our [severity guidelines](https://bounty.github.com/rewards) for more information about how severities are calculated.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Remote code execution via protocol handlers such as `ghapp://`
* Code execution without user interaction such as when cloning or fetching malicious repositories
* Code execution that requires minimal, expected user interaction, such as performing actions on a repository that a user would not expect to lead to code execution

## Out of scope

Explicitly excluded for this product.

* Code execution requiring social-engineering or unlikely user interaction is typically not eligible for rewards.
* Vulnerabilities which do not trigger code-execution are out-of-scope and ineligible for reward.

