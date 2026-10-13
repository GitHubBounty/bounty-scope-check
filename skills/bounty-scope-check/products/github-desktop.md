# GitHub Desktop

Canonical page: https://bounty.github.com/targets/github-desktop

## Synopsis

[GitHub Desktop](https://desktop.github.com) is an open-source [Electron](https://electronjs.org)-based app for working with your GitHub.com or GitHub Enterprise account. It uses the [`dugite`](https://github.com/desktop/dugite) and [`dugite-native`](https://github.com/desktop/dugite-native) libraries for performing git operations.

Even if the issue you identified is out-of-scope and ineligible for our bounty program, we encourage you to [open an issue upstream](https://github.com/desktop/desktop). Please see our [severity guidelines](https://bounty.github.com/rewards) for more information about how severities are calculated.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Remote code execution via protocol handlers such as `x-github-client://`
* Code execution without user interaction such as when cloning or fetching malicious repositories
* Code execution that requires minimal, expected user interaction, such as performing actions on a repository that a user would not expect to lead to code execution

## Out of scope

Explicitly excluded for this product.

* Code execution requiring social-engineering or unlikely user interaction is typically not eligible for rewards.
* Vulnerabilities which do not trigger code-execution are out-of-scope and ineligible for reward.

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Cloning a repository you do not trust

Adding or cloning a repository means letting Git process repository content that its author controls. It does not copy the attacker's `.git/hooks` or `.git/config` into the new working copy. Desktop is a Git client, so reports where the whole chain is "the user cloned my repository and then Git processed the repository content as designed" are ineligible. A report may be eligible if Desktop mishandles that content, runs something Git would not have, or crosses a security boundary before the user has taken any action on the repository.

### Code execution that needs the user to be talked into it

Chains that require the user to open a specific file, change a setting, approve a prompt they had a reason to refuse, or follow instructions from the attacker are social engineering. If your report includes a step like this, describe it plainly and explain why the user would realistically take it.

### Anything that needs local access first

An attacker who can already write to your disk or run as your user can read Desktop's stored credentials, edit its configuration, and replace its files. Reports that describe reading a token from local storage, or modifying local state to change behaviour, are ineligible without showing how a remote attacker reaches that state.

### The OAuth client identifier

Desktop is a public client, so its client ID is embedded in the application and is not a secret. Reports that it can be extracted are ineligible.

