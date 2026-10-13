# Severity and reward guidance

All bounty submissions are rated by GitHub using a purposefully simple scale. Each vulnerability is unique, but the following is a rough guideline we use internally for rating and rewarding submissions across the public and private programs:

Claimed severity does not determine the reward. Severity is assessed independently based on demonstrated impact.

## Critical

Public programs: $10000. Private programs: $30000+.

Critical severity issues present a direct and immediate risk to a broad array of our users or to a GitHub product itself. They often affect relatively low-level/foundational components in one of our application stacks or infrastructure. For example:

* arbitrary code/command execution on a server in our production network
* arbitrary SQL queries on a production database
* bypassing the login process, either password or 2FA
* access to sensitive production user data or access to internal production systems
* accessing another user's data in the GitHub Actions service

The amount listed for critical vulnerabilities is only a guideline, and GitHub may reward higher amounts for exceptional reports.

## High

Public programs: $5000. Private programs: $20000.

High severity issues allow an attacker to read or modify highly sensitive data that they are not authorized to access. They are generally more narrow in scope than critical issues, though they may still grant an attacker extensive access. For example:

* injecting attacker controlled content into GitHub.com (XSS) that bypasses CSP
* bypassing authorization logic to grant a repository or package collaborator more access than intended
* discovering sensitive user or GitHub data in a publicly exposed resource, such as an S3 bucket
* overwriting a customer repository or package that should be inaccessible
* gaining access to a non-critical resource that only employees should be able to reach
* using the GitHub Actions repo-scoped GitHub token to access high-risk private content outside of that repository
* sending authentication credentials from a client app to an unintended server
* code execution in a client app that requires no user interaction, such as arbitrary code execution upon repo clone or via a protocol handler

## Medium

Public programs: $2000. Private programs: $7500.

Medium severity issues allow an attacker to read or modify limited amounts of data that they are not authorized to access. They generally grant access to less sensitive information than high severity issues. For example:

* disclosing the title of issues in private repositories, which should be inaccessible
* injecting attacker controlled content into GitHub.com (XSS) but not bypassing CSP or executing sensitive actions with another user's session
* bypassing CSRF validation for low risk actions, such as starring a repository or unsubscribing from a mailing list
* code execution in a client app that requires minimal, expected user interaction, such as performing actions on a repository or [with a package](https://docs.npmjs.com/cli/v7/using-npm/config#ignore-scripts) that a user would not expect to lead to code execution
* package integrity compromise, i.e., downloading a package that does not match the integrity as defined in `package-lock.json`

## Low

Public programs: $250. Private programs: $1000.

Low severity issues allow an attacker to access extremely limited amounts of data. They may violate an expectation for how something is intended to work but allow nearly no escalation of privilege or ability to trigger unintended behavior by an attacker. For example:

* signing up arbitrary users for access to an "early access feature" without their consent
* creating an issue comment that bypasses our image proxying filter by providing a malformed URL
* triggering verbose or debug error pages without proof of exploitability or obtaining sensitive information
* triggering application exceptions that could affect many users
* injecting JavaScript event handlers into links, etc., that are mitigated by CSP on GitHub.com
* disclosing the existence of private packages on npm that should be inaccessible, e.g., through error messages (but not through timing attacks, which are ineligible)
* novel supply chain vulnerabilities that affect a GitHub product but are not solely limited to that product
* credentials such as those from the `.npmrc` file or from GitHub Enterprise Server being leaked in logs

## Defense in depth

Reward: GitHub swag, no cash bounty.

Defense in depth is a narrow category. It applies only when a report demonstrates that a security control GitHub intended to enforce reproducibly fails, but another independent protection prevents that failure from causing user impact.

The report must identify the intended security control, show the behavior it is supposed to prevent, and demonstrate the control failing. A product bug, unexpected behavior, unnecessary exposure, missing optional hardening, or deviation from a security best practice is not defense in depth merely because it is interesting or could be described in security terms.

Examples that may qualify include:

* an authorization check that can be bypassed, where a separate authorization check still prevents access
* an isolation boundary that demonstrably fails, where another boundary prevents access to sensitive state
* an input restriction intended to block a security-sensitive action that can be bypassed, where downstream enforcement still blocks the action

If the report does not demonstrate the failure of an intended security control, it does not qualify for this tier. Do not use defense in depth as a catch-all for findings with no demonstrated impact.

Qualifying defense in depth reports that result in a code or documentation fix receive GitHub swag rather than a cash bounty. If a failed control can be turned into demonstrated user impact, the finding is rated under the Low through Critical tiers instead.

