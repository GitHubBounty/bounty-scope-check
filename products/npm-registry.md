# npm Registry

Canonical page: https://bounty.github.com/targets/npm-registry

## Synopsis

The npm Registry includes subdomains under `*.npmjs.com` and `*.npmjs.org`. These are services related to serving npm packages to external users and other support for npm.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

- Vulnerabilities that lead to account takeover
- Novel supply chain vulnerabilities
- Gaining access to private packages that should be inaccessible
- Disclosing the existence of private packages that should be inaccessible, e.g., through error messages (but not through timing attacks, which are ineligible, as described below)

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Vulnerabilities in packages that are hosted on the registry

npm users are responsible for the content hosted in their packages. Any vulnerabilities in user content do not affect the security of npm or its users. We recommend that you report these vulnerabilities directly to the owner of the package.

### Malicious packages

npm users are responsible for vetting the content of packages that they choose to install. However, npm takes its responsibility as steward of the JavaScript ecosystem seriously; therefore, we actively scan for malware in the registry. If you do happen to find a malicious package that has yet to be removed, please [contact support](https://support.github.com/request).

### Infrastructure vulnerabilities

Infrastructure vulnerabilities such as an outdated version of Transport Layer Security (TLS) or a lack of rate limiting are considered out of scope for this bounty program unless you are able to prove privilege escalation or the ability to use it as part of a larger, more impactful attack.

### Timing attacks that reveal a private package

Architectural nuances prevent us from systematically preventing timing attacks from determining whether a specific package exists. Therefore, timing attacks are considered ineligible.

### Account takeover that depends on the victim acting

Reports described as account takeover must work against a user who is behaving normally. Chains that need the victim to enter their password into a page you control, click a link you sent them, accept an invitation, or hand over a token or one-time code are social engineering rather than a flaw in npm. If the victim has to help, say so plainly in the report and explain why the step is realistic.

### Publicly available package and user data

Package names, versions, publish timestamps, dependency lists, maintainer usernames, and the contents of public packages are all intentionally public. The same applies to publisher email addresses where the publisher has chosen to make them visible. Reports that this data can be collected or enumerated are ineligible without a demonstrated impact beyond its availability.

### Organization invitations and membership changes

Invitations, membership removal, and ownership transfer behave as designed, including that an invitation sent to an email address can be accepted by whoever controls that address. Reports that a member can be added or removed by someone with the permission to do so are not vulnerabilities.

### Account ownership disputes

Lost accounts, accounts registered against an email address you own, and disputes over a package name are handled by [support](https://support.github.com/request) rather than the bounty program.

### Revoking a token you already know the identifier for

Being able to revoke a token whose unguessable identifier you already hold is a known low risk. The result is that the owner has to create a new token, which is inconvenient rather than a compromise. These reports are ineligible unless you can show the identifiers are predictable or enumerable, or that you can use the token rather than only destroy it.

