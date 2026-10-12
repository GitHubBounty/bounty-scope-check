# GitHub Credentials

Canonical page: https://bounty.github.com/targets/github-credentials

## Synopsis

GitHub, Inc. uses a mix of our own physical infrastructure, cloud platforms and third-party services to keep everything running smoothly. Keeping credentials and access tokens secure for these resources is paramount to the security of our employees and users.

Please review our [guidance for handling PII](https://bounty.github.com/rules#handling_personally_identifiable_information_pii) before investigating credentials allowing access to GitHub, Inc resources. The reward amount is based on the impact of the leaked credential which will be determined by the GitHub Security team.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Credentials allowing access to cloud services, package managers and other resources used by GitHub, Inc employees
* Credentials accidentally made public in repositories which allow access to GitHub, Inc resources. This does *not* include credentials exposed by our users and credentials which do not allow access to GitHub, Inc resources.
* Credentials exposed by third-party services which allow access to GitHub, Inc resources

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Credentials which have been detected by GitHub Secret Scanning

[GitHub Secret Scanning](https://docs.github.com/en/code-security/concepts/secret-security/secret-scanning) automatically detects credentials accidentally committed to repositories for a number of service providers. Credentials for GitHub, Inc. resources that have already been found through this feature are ineligible for reward.

### Credentials on GitHub

Credentials exposed by our users are not in scope for our bounty program. We automatically scan public repositories for leaked credentials, and we strongly encourage developers to enable [GitHub Advanced Security Scanning protections](https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning?learn=secret_scanning&learnProduct=code-security) on their private repositories to do the same. 

Additionally, you can use [this REST API](https://docs.github.com/en/rest/credentials/revoke?apiVersion=2022-11-28#revoke-a-list-of-credentials) to revoke any credentials you discovered without authentication.

### Credentials you have not confirmed still work

We need to know that a credential is live and what it reaches. Do not test beyond the minimum needed to confirm validity, but do tell us what you did confirm: which service it belongs to, what a successful call returned, and roughly what access it implies. A string that looks like a key, or a hit from a scanner with no validation behind it, is ineligible. Never use a credential to read data, change state, or move further into our systems.

### Values that are not secrets

Public API keys, client identifiers for public OAuth apps, analytics and telemetry tokens, keys scoped to a single public dataset, and credentials for services with no GitHub data behind them are ineligible even when they are clearly ours. The same applies to keys that appear in a commit but were rotated before you found them.

### Secrets inside GitHub Actions

Actions secrets are available to the workflows in the repository that owns them, and are redacted from logs on a best effort basis. Reports that a workflow you can modify can read the secrets available to it, or that an unusual encoding defeats log redaction, are ineligible. Redaction is a convenience, not a boundary: treat any secret a workflow can read as readable by anyone who can change that workflow.

