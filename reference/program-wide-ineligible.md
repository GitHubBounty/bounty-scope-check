# Program-wide ineligible submissions

These apply to every product, regardless of what an individual product page says. A finding matching any of them is ineligible even if the affected product is in scope.

There are a handful of reports that we consider ineligible, either because the feature is working as intended or we accept the low risk as a security/usability tradeoff:

## OAuth client ID and secrets are publicly available in desktop and mobile apps

It is expected that GitHub-owned clients, such as [GitHub Mobile](https://bounty.github.com/targets/github-for-mobile) and [GitHub CLI](https://bounty.github.com/targets/github-cli), include both the OAuth client ID and OAuth secret. These are public clients, and a public client cannot hold a secret. Recovering one by unpacking an app, reading a binary, or watching traffic is not by itself a vulnerability, and a report that stops there is not eligible.

A working chain that turns the secret into access to an account someone else owns is eligible, and we have rewarded reports of that kind. If you can intercept the OAuth callback from another application on the device and obtain a token for an account you do not control, we want to see it. Tell us the platform and the exact redirect target you intercepted, because a custom URL scheme and a verified Universal Link or App Link do not give the same guarantees.

## Use of known-vulnerable software

GitHub has a dedicated team responsible for tracking and remediating the use of known-vulnerable software. Submissions related to GitHub services using known-vulnerable software are only eligible 30 days after public disclosure of a vulnerability. In addition, any submissions related to using known-vulnerable software must show evidence of exploitability. Simply demonstrating that GitHub is running a known vulnerable version is not sufficient, the submission must demonstrate an actual impact of exploitation like disclosing private data.

## Vulnerability in upstream dependencies

Vulnerabilities that are due to a vulnerability in an upstream dependency are out of scope and should instead be disclosed to the upstream maintainers. We may make exceptions for vulnerabilities that have a substantial impact to our production environment and customer data, however, issues should still be directed to the maintainers of the dependency upstream first.

## Clickjacking a static site

Several GitHub owned sites are created using a static site generator and hosted on [GitHub Pages](https://pages.github.com/). These applications do not contain any sensitive user information or authenticated sessions. As a result, this does not present a security risk.

## Local Access

Vulnerabilities that require local system access are out of scope and ineligible for bounty across all services.

## Network Denial of Service

Network-level and volumetric denial of service attacks (e.g., DDoS, traffic flooding) are not allowed and are ineligible for reward. We have mitigation plans in place for these types of attacks. Application-layer denial of service vulnerabilities (e.g., ReDoS, logic bombs) are eligible. Please see our [rules](https://bounty.github.com/rules) for guidelines on how to research these responsibly.

## Cache purging and cache eviction

Reports that you can cause a cached object to be evicted from one of our CDN edges are ineligible. Eviction does not change what we serve. The next request fetches the same content from origin and caches it again, so the result is a cache miss and some additional origin traffic, which our infrastructure is built to absorb. This includes reports where the impact is framed as denial of service.

Cache poisoning is a different finding and is eligible. If you can make a cache serve content **you** control to another user, or return one user's private content to another, that crosses a security boundary and we want the report. The distinction is whether you are removing a cached copy or replacing it.

## Content that stays cached after you delete it or make it private

When you delete a file, delete a repository, change a repository from public to private, remove a member from an organisation, or replace an avatar, the original content can remain reachable from our caches and CDNs for a short period afterwards. We have received this report many times, against raw file content, Git LFS objects, rendered notebooks, avatars, link previews, release downloads and gists.

Caches expire rather than being erased everywhere at the moment you make a change, so a copy that was public a moment ago can still be served for a short window. Treat anything that has been public as public. Once content has been served we cannot guarantee that every cached copy of it disappears the instant you change your mind.

Reports that a recently deleted or newly private object is briefly still served are ineligible, including reports that rely on cache status shown in response headers.

Content that was public stays public. Replacing or deleting an avatar, a release asset, a gist or a file that anyone could already fetch does not make the old copy private, so a cached copy of it still being reachable is not an exposure.

It is eligible, and we want the report, if you can reach content that was never public. Where content has been made private, it is eligible if it remains reachable substantially beyond normal cache expiry. If you can retrieve private repository content without a valid, unexpired signed URL, that is a finding regardless of how it got into the cache.

## Git hooks, filters, and local repository configuration

Git is designed to run code that lives in a repository. Hooks, clean and smudge filters, and `core.hooksPath` all execute by design, and a repository's local configuration deliberately takes precedence over the global and system files. Demonstrating that in a repository you created yourself is not a finding, and neither is a chain where the victim has to run a `git config` command that the attacker wrote into a README.

Two details are worth checking before you write one of these up. `.git/hooks` and `.git/config` are not copied by `git clone`, so an attacker cannot plant either of them in somebody else's working copy that way. And hooks in the default `.git/hooks` directory run whether or not `core.hooksPath` is set, so if your proof of concept puts them there, the configuration change is not what made the code run.

What may be eligible is one of our clients doing something unsafe with repository content on its own. We have rewarded a repository name being interpolated into a shell command, a recursive clone reaching a submodule the user never asked for, an artifact extraction that overwrote `.git/config`, and a configuration file that was read before the trust prompt meant to gate it. Cloning a repository, opening it in a client, or checking out a branch does not by itself make a chain eligible. The report must show the client crossing a security boundary beyond the behavior the user authorized and the product is designed to perform. Following setup instructions the attacker put in a README is not eligible.

## Attacks that require following an attacker's instructions

Viewing an issue or pull request, cloning or opening a repository, checking out a branch, and reviewing a contribution neither automatically qualifies nor disqualifies a report. Eligibility depends on the specific product, its security model, the warnings or prompts shown, what the action inherently authorizes, and whether GitHub or a GitHub client crosses a security boundary beyond that authorization.

Following instructions supplied by the attacker is different. Reports are ineligible when the chain requires the victim to copy and paste a command into a terminal or developer console, run a script or executable from the attacker, change a security setting, install an extension, grant additional permissions, or approve a warning that explains the risk. In those cases the user is executing or authorizing the attack rather than the product crossing a security boundary.

Describe every required user action exactly. Replacing "the victim pastes and runs my command" with "the victim interacts with a malicious repository" does not make the interaction a vulnerability.

## Typosquatting

Typosquatting on domains similar to GitHub official domains are out of scope and ineligible for bounty. If you would like to report a domain, please report to our [support team](https://support.github.com/request).

## Vulnerabilities identified in Open Source Repositories

Most open source repositories are outside the scope of our bug bounty program. The repository's [SECURITY.md](https://docs.github.com/en/code-security/getting-started/adding-a-security-policy-to-your-repository) describes the best avenue for reporting vulnerabilities in open source projects. Please ensure to submit your report to the place outlined in the file.

## Assets that are not owned by GitHub

This is one of the most common reasons we close a report. Only the applications and domains listed in our [scope](https://bounty.github.com/scope) are eligible, and an asset is not ours simply because it is named after us, linked from a repository, or referenced by our documentation.

Please confirm ownership before you submit. Reports about storage buckets whose name contains "github", preview deployments and third-party hosting linked from a repository, Microsoft or Azure services, and vendor tooling running on a subdomain are all regularly closed for this reason. The same applies to credentials: a key committed by one of our users is not a GitHub credential. See [GitHub Credentials](https://bounty.github.com/targets/github-credentials.html) for what we do consider in scope.

## Abuse of a service is not automatically a vulnerability

Some findings describe getting more of something than you are entitled to, rather than crossing a security boundary. Bypassing a usage limit or quota, resetting a trial, avoiding a charge, consuming another account's allowance, or provoking our moderation and enforcement systems into acting against someone are handled as abuse rather than through the bounty program.

These are ineligible unless you can show a security impact alongside the abuse, such as access to another user's data, an authorization bypass, or a material financial loss to GitHub. Please report abuse through [support](https://support.github.com/request).

## Attacks that require intercepting or modifying traffic

Reports whose impact depends on an attacker controlling what GitHub sends to another user over the network are ineligible. If the attack requires a machine-in-the-middle position, a modified API response delivered to the victim, or a certificate added to the victim's trust store, then you are demonstrating what happens when transport security is already defeated rather than a flaw in our products.

Using an intercepting proxy or browser developer tools locally to simulate a plausible content-injection point while testing a separate security control, such as GitHub.com's Content Security Policy, is permitted and does not make the report ineligible by itself. The report must still demonstrate that the intended control can be bypassed in a location where content injection could realistically occur.

