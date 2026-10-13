# GitHub API

Canonical page: https://bounty.github.com/targets/github-api

## Synopsis

The GitHub APIs are used by thousands of developers and applications to programmatically interact with GitHub data and services. Because so much of GitHub.com functionality is exposed through the APIs, security has always been a high priority.

GitHub provides both a [REST API](https://docs.github.com/en/rest) and a [GraphQL API](https://docs.github.com/en/graphql).

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Privilege escalation via [GitHub Apps](https://docs.github.com/en/apps/creating-github-apps) or [OAuth Apps](https://docs.github.com/en/apps/oauth-apps)
* Accessing private resources without a [`repo`-scoped](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/scopes-for-oauth-apps#available-scopes) token
* Accessing team discussions without a [`read:discussion`-scoped](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/scopes-for-oauth-apps#available-scopes) token
* Bypassing GraphQL [rate and query limits](https://docs.github.com/en/graphql/overview/rate-limits-and-query-limits-for-the-graphql-api)
* Accessing SAML SSO protected organization data with [an unauthorized personal access token](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-single-sign-on/authorizing-a-personal-access-token-for-use-with-single-sign-on)
* Bypassing an organization's [OAuth app access restrictions](https://docs.github.com/en/organizations/managing-oauth-access-to-your-organizations-data/enabling-oauth-app-access-restrictions-for-your-organization) to allow untrusted apps to access organization resources

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Write access to a repository includes configuring its secrets

It is intentional that write access to a repository allows users to list Actions secret metadata, retrieve the public key used to encrypt secrets, and create, update, or delete secret values, as [documented in the REST API reference](https://docs.github.com/en/rest/actions/secrets). Users with write access are expected to be able to create and edit workflows, which requires being able to configure the secrets those workflows use.

Existing plaintext secret values cannot be read back. A report showing that a write-access user can retrieve one is not covered by this exclusion.

### Data from public repositories returned by the API

Content in a public repository is public, including through the API. Reports that an API endpoint returns source code, file contents, commit history, or other data belonging to a public repository are not vulnerabilities. This applies even where the same data is harder to reach through the web UI. To be eligible, a report must show the API returning data from a **private** resource to a user who is not authorised to see it.

### Repository and organization metadata

Metadata such as repository names, timestamps, counts, language statistics, topic tags, and similar attributes is not treated as sensitive. Reports that the API discloses metadata, without showing access to private content or a privilege escalation, are ineligible.

### Functionality disabled in the UI but reachable through the API

Features may be turned off in the web UI, for example wikis or projects, without that being a hard security boundary. Reaching the equivalent functionality through the API is generally ineligible. See [accessing certain disabled functionality](https://bounty.github.com/ineligible#accessing_certain_disabled_functionality) for the full explanation.

### Email addresses returned by the API

There are several ways to determine that an email address is in use on GitHub, and we have accepted that risk in exchange for usability. Commit author email addresses in particular are set by the developer and are used for attribution, which is explained under [impersonating a user through git email address](https://bounty.github.com/ineligible#impersonating_a_user_through_git_email_address). Reports about email addresses being visible or enumerable through the API are ineligible unless you can show a private email address being disclosed to a user who should not have it.

