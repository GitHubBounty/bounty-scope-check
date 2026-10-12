# GitHub.com

Canonical page: https://bounty.github.com/targets/github

## Synopsis

[GitHub.com](https://github.com) is our main web site. It is our most intricate application with a number of user inputs and access methods. GitHub.com is built on Ruby on Rails and leverages a number of Open Source technologies.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Escalating from repository admin to organization admin
* Bypassing [repository permissions in an organization](https://help.github.com/articles/repository-permission-levels-for-an-organization/), such as making a repository public without admin permissions
* Bypassing [branch protection settings](https://help.github.com/articles/about-protected-branches/) in a repository
* Collaboration features such as [project boards](https://help.github.com/articles/about-project-boards/) and [team discussions](https://help.github.com/articles/about-team-discussions/)
* XSS caused by our markdown pipeline which takes [GFM-flavored markdown](https://github.com/github/cmark-gfm) and produces sanitized HTML
* Package ecosystem features such as [GitHub Package Registry](https://help.github.com/en/github/managing-packages-with-github-package-registry/about-github-package-registry)
* Community-and-safety features, such as bypassing privacy controls (e.g. revealing another user's private email address)
* Importing existing Git, Subversion, Mercurial and TFS repositories with [GitHub Importer](https://help.github.com/articles/importing-a-repository-with-github-importer/)
* Authorization bypasses in GitHub's SSH components
* Server Side Request Forgery vulnerabilities allowing access to our internal network. You may use `ssrf-target.iad.github.net` to test out SSRF attacks.

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Including HTML in Markdown content

Many areas of GitHub allow content formatted in [GitHub Flavored Markdown](https://help.github.com/articles/about-writing-and-formatting-on-github/). It is intended that these Markdown fields allow a limited subset of HTML, such as `<b>`, `<sup>` and `<details>`. HTML included by users in Markdown fields is filtered for malicious input such as `<script>`, so this does not present a security risk. However, if you are able to demonstrate that you are able to perform malicious actions via the HTML tags, please submit a report, as this may be eligible for bounty.

### Leaking email addresses via .patch links

`.patch` links on GitHub show the raw commit diff, similar to `git-format-patch`, and intentionally show the email address used by the author. The email address shown in `.patch` links is configured by the user with `git-config` on their local machine. To hide email addresses from Git operations, such as `.patch` links, users can set the `Keep my email address private` and `Block command line pushes that expose my email` options. More details are available in our [About Commit Email Addresses](https://help.github.com/en/articles/setting-your-commit-email-address#about-commit-email-addresses) documentation.

### Phishing using Unicode homoglyphs, RTLO, or non-printable characters

We are aware of different ways that Unicode - specifically homoglyphs, RTLO, and non-printable characters - can be used to display misleading information to other GitHub users. We consider these low-risk and ineligible for a reward. If you have noticed someone using GitHub for phishing, please let us know by reporting it as abuse through our [support portal](https://github.com/contact/report-abuse).

### Email verification policy

Any email address that is not already associated with an account on GitHub may be claimed and this will give commit attribution to the claiming user. While we allow this attribution without requiring email address verification, any disputes around emails on accounts can be resolved by contacting our [support team](https://github.com/contact/report-abuse).

### Email Invitations

It is intentional that invitations sent via email can be claimed with any user account. If you wish to invite a specific GitHub user, that user should be invited directly by username.

### Impersonating a user through git email address

Because Git is a distributed version control system, GitHub must use the commit email address to assign attribution. When you push a repository to GitHub.com it may contain one or more commits, some of which you may not have authored. For example, imagine a scenario where you collaborated with a number of people on a git repository before you made your first push of that repository to GitHub.com. This push would contain a number of commits from several authors. It would be incorrect to assign all of the commits to the person doing the push, so we use the commit log email addresses to assign attribution on GitHub.com. Each subsequent push to GitHub uses this same logic to assign attribution of commit authors.

It's important to note that impersonating another GitHub user in this fashion doesn't grant you access to any of their repositories or give you any privileges you didn't already have. However, GitHub does consider impersonation an account abuse issue that we take very seriously. If someone is wrongfully impersonating you, please [let us know by contacting our support team](https://github.com/contact) and we will investigate the matter and deal with it as quickly as we can. In addition, if you are still concerned about this, you and your team can choose to use Git's built in options to sign commits with a GPG key (check out the `git commit -S` command).

### DMARC, SPF and DKIM email policy

Our DMARC, SPF and DKIM settings are tuned to balance security against email deliverability concerns. We continue to evaluate our setup and may make this functionality more strict in the future.

### Bypassing country restrictions for SMS two-factor authentication

The restriction on which countries are able to configure SMS two-factor authentication is based on SMS delivery reliability. We have removed countries we found to have low delivery success rates to prevent account lockout. Our validation is client-side and bypassing this validation does not present a security risk. Users in countries where SMS is unavailable can use an alternative [two-factor authentication method](https://help.github.com/articles/configuring-two-factor-authentication/)

### Vulnerabilities in repositories hosted on GitHub

GitHub users are responsible for the content hosted in their repositories. Any vulnerabilities in user content do not affect the security of GitHub.com or its users. We recommend that you report these vulnerabilities directly to the owner of the repository.

### Host header injection

Host header injection reports are ineligible unless it can be shown to cause a specific security issue. We set the `Strict-Transport-Security` header and are in the browser preload lists, which prevent active network attacks that may attempt to inject the header.

### Timing attacks which reveal a private repository or user

There are architectural nuances that prevent us from systematically preventing timing attacks from determining if a specific repository exists, or if a specific user is part of a [secret team](https://help.github.com/articles/about-teams/), and are therefore ineligible.

### 2FA does not invalidate existing sessions

Enabling 2FA does not imply that an account may have been compromised, and as a result, we do not reset all existing sessions. If a user changes/resets their password GitHub will reset all existing sessions.

### Enabling 2FA without a verified email

Enabling 2FA without a verified email is allowed. While this could prevent someone from using that email address, we consider this a spam and abuse issue.

### Vulnerabilities caused by out-dated browsers

Vulnerabilities that don't affect the latest version of modern browsers, such as Chrome, Firefox, Edge and Safari, are ineligible. Vulnerabilities caused by browser extensions are also ineligible.

### Camo image proxy

Our "Camo" system is used to proxy images included in Markdown fields via `githubusercontent.com`. We rely on the isolation of `githubusercontent.com` and the fact that we don’t send any cookies to that domain. These images are untrusted and we intentionally do not attempt to modify or filter the response. We don’t consider the ability to make requests to external services a security risk, as an attacker can perform this in many other ways without using GitHub’s image proxy, so reports that stop at "GitHub fetched my URL" are ineligible. The proxy is intended to run where it cannot reach internal addresses, and that restriction is a control we do defend: if you can get it to reach an internal host or port, or to distinguish internal hosts by their responses or timing, that is eligible and we want the report.

### Lack of Sudo mode

We use [Sudo mode](https://help.github.com/en/github/authenticating-to-github/sudo-mode) to ensure legitimate users are taking certain high risk actions. If we have not included sudo mode on an endpoint, we have likely accepted its risk and most submissions will be ineligible.

### Community and safety bypasses that do not affect privacy

GitHub employs a number of community and [safety](https://help.github.com/en/github/building-a-strong-community/maintaining-your-safety-on-github) features, such as blocking users or locking conversations on issues/discussions/etc.  In most cases, bypasses of these features via some edge case will not result in a bounty reward unless there is a privacy (confidentiality) breach. For example, bypassing the 24 hour interaction limit at 23 hours and 10 minutes will be ineligible. However, if you are able to bypass controls and reveal another user's *private* email address, that may be eligible.

### Activity in archived repos

Submissions related to archived repos that do not demonstrate the ability to change the actual content in the repo (e.g. adding/removing collaborators, modifying some repo settings) will be ineligible. The same for submissions that do not demonstrate the ability to change ownership or the actual archived status.

### Accessing certain disabled functionality

Some features may be disabled on GitHub in the UI and that ability (to disable) is more of a convenience than a hard security boundary. Projects and wikis are two examples of this. Accessing those disabled features through the API or some other technique are not eligible for a bounty reward. Being able to access functionality that is not available to underprivileged users is eligible.

### Lack of rate limiting

As stated elsewhere, submissions around volumetric DoS attacks are not in the scope of our bounty program. Submissions citing lack of rate limiting will be treated similarly. We generally consider such activity spammy or abusive behavior, and have a dedicated team for addressing such issues.

### Email and Username Enumeration

There are multiple ways on GitHub.com to determine whether an email address or username is in use. We have accepted this risk to improve our users' experience.

### OAuth App Redirect

Redirecting the user to the registered callback URL is part of the OAuth specification, and is therefore expected behavior. It is up to users to know and trust the OAuth app that they are authorizing.

### Lack of Secret Scanning Alert

GitHub has a list of [supported secret scanning patterns](https://docs.github.com/en/code-security/secret-scanning/introduction/supported-secret-scanning-patterns) in order to identify secrets. If the scanner is not detecting secrets using the default patterns, we encourage you to [create custom patterns for secret scanning](https://docs.github.com/en/code-security/secret-scanning/using-advanced-secret-scanning-and-push-protection-features/custom-patterns/defining-custom-patterns-for-secret-scanning).

### Product bugs and input validation without a security impact

Not every bug is a vulnerability. A form that accepts a malformed value, a setting that displays confusingly, a field that could validate more strictly, or an interface that behaves unexpectedly are product bugs, and [support](https://support.github.com/request) is the right route for them.

These become eligible when you can name what an attacker gains. If the change only happens after the account owner opens the page and saves it themselves, or the malformed value is only ever shown back to you, there is no security boundary being crossed.

### Issue and pull request templates and prefilled query parameters

Issue and pull request creation accepts query parameters that prefill the title, body, labels, assignees and template selection. A link can therefore open a form with content the author of the link chose. Nothing is created until the person clicking it reviews the form and submits it themselves, and the resulting issue is attributed to them.

Reports that a crafted link prefills a form, selects a different template, or skips a template chooser are ineligible. To be eligible, show the parameters creating or modifying something without the user submitting it, or granting access the user does not already have on that repository.

### Deploy keys and repository rulesets

A deploy key with write access is repository owner automation. It acts in the owner's context, so where a ruleset already lists the repository owner or an owner-owned app as a bypass actor, a write deploy key inherits that bypass. This is the configuration working as set, not a way around it.

Check the ruleset's bypass list before reporting. To be eligible, show a ruleset being bypassed by an actor that is not on that list, or a key acting on a repository it was never added to.

### Impersonation through profile names and naming patterns

Display names, usernames, biographies, and avatars are chosen by the account holder and are not a statement that we endorse anyone. Accounts that resemble GitHub staff, our triage team, or an official programme are a known abuse problem rather than a technical vulnerability, and reports whose impact depends on someone believing a profile is official are ineligible. Please report accounts impersonating GitHub through [support](https://support.github.com/request).

