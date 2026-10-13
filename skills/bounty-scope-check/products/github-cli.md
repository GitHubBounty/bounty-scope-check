# GitHub CLI

Canonical page: https://bounty.github.com/targets/github-cli

## Synopsis

[GitHub CLI](https://cli.github.com) is an open source command line tool for working with your GitHub.com account. It is built with Golang, and performs several GitHub.com commands from your terminal, such as viewing, commenting and performing other actions on issues and PRs.

Even if the issue you identified is out-of-scope and ineligible for our bounty program, we encourage you to [open an issue upstream](https://github.com/cli/cli). Please see [our severity guidelines](https://bounty.github.com/rewards) for more information about how severities are calculated.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Code execution without user interaction such as when cloning or fetching malicious repositories
* Code execution that requires minimal, expected user interaction, such as performing actions on a repository that a user would not expect to lead to code execution
* Leakage of credentials to an external attacker without access to the local system

## Out of scope

Explicitly excluded for this product.

* Code execution requiring social-engineering or unlikely user interaction is typically not eligible for rewards.
* Vulnerabilities which require local system access, such as local credential storage issues, etc.

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Anything that needs local access first

An attacker who can already run commands as you, read your files, or set your environment variables has everything the CLI has. Reading the token out of the config file or the keyring, setting `GH_TOKEN` or `GH_HOST`, or editing the config to change where requests go are all consequences of that access rather than separate vulnerabilities. To be eligible, a report needs to show an attacker **without** local access obtaining credentials or execution.

### Extensions, aliases, and anything you install

`gh extension install` and `gh alias set` run code you have chosen to install, and extensions are ordinary repositories written by other people. That the code then runs is the intended behaviour, not a sandbox escape. Reports that an installed extension or a configured alias can act with your credentials are ineligible.

### Tokens sent to the host you configured

The CLI sends your credentials to the host it is configured to talk to, including GitHub Enterprise Server hosts you have authenticated against. Reports that a token is sent to a configured host, or that a token works against the API it was issued for, are working as designed. A report is eligible if you can show credentials for one host being sent to a different host.

### Cloning or checking out an untrusted repository

Cloning a repository means running its content through Git, and Git is designed to let repositories configure their own behaviour. See [our position on repositories you do not trust](https://bounty.github.com/ineligible) before reporting. A report is eligible if the CLI does something Git itself would not, or if execution happens without the user taking any action on the repository.

