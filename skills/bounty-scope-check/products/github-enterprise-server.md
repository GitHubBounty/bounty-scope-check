# GitHub Enterprise Server

Canonical page: https://bounty.github.com/targets/github-enterprise-server

## Synopsis

GitHub Enterprise Server is the on-premise version of GitHub Enterprise. GitHub Enterprise Server shares a code-base with GitHub.com, is built on Ruby on Rails and leverages a number of open source technologies. GitHub Enterprise Server adds a number of features for enterprise infrastructures, including additional authentication backends and clustering options.

You can request a trial of GitHub Enterprise Server for security testing at [https://enterprise.github.com/bounty](https://enterprise.github.com/bounty). Code de-obfuscation may be explored to further investigate GitHub Enterprise Server but only for the purpose of the bounty program.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Bypassing instance-wide authentication, also known as [*private mode*](https://help.github.com/enterprise/admin/guides/installation/enabling-private-mode/)
* External authentication backends including [CAS, LDAP, and SAML](https://help.github.com/enterprise/admin/guides/user-management/)
* In-app administration of the instance using a site administrator control panel
* [User, organization, and repository migration](https://help.github.com/enterprise/admin/guides/migrations/)
* [Web-based management console](https://help.github.com/enterprise/admin/guides/installation/web-based-management-console/) and [SSH access](https://help.github.com/enterprise/admin/guides/installation/administrative-shell-ssh-access/) to configure and update the instance
* [Pre-receive hook scripts](https://help.github.com/enterprise/admin/guides/developer-workflow/creating-a-pre-receive-hook-script/)
* [GitHub Connect](https://help.github.com/enterprise/admin/guides/developer-workflow/connecting-github-enterprise-server-to-github-com/) allows users to share specific features and workflows between your GitHub Enterprise Server instance and a GitHub.com organization on GitHub Enterprise Cloud.
* See [our documentation](https://help.github.com/enterprise/admin/guides/installation/network-ports-to-open/) for a list of services typically open on an instance.

## Out of scope

Explicitly excluded for this product.

* `https://enterprise.github.com/login` is a separate management portal for GitHub Enterprise Server customers and is not in-scope at this time.
* Vulnerabilities not present in latest patch release of each non-deprecated version of GitHub Enterprise Server. Major versions of GitHub Enterprise Server are deprecated one year after release. For more information see [the GitHub Enterprise Server release schedule](https://docs.github.com/en/enterprise-server@latest/admin/all-releases).

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Vulnerabilities caused by lack of subdomain isolation

Vulnerabilities present in GitHub Enterprise Server when [subdomain isolation](https://docs.github.com/en/enterprise-server@3.16/admin/configuring-settings/hardening-security-for-your-enterprise/enabling-subdomain-isolation?learn=improve_security_of_your_instance&learnProduct=admin) is disabled. GitHub recommends that all GitHub Enterprise Server installations should have subdomain isolation enabled.

### Escalation to the root user via sudo

Administrative SSH access grants `sudo` to be used to escalate to root permissions. Given this existing level of privilege, local escalation of the administrative account to root permissions is *not* considered in scope.

### Access to sensitive configuration information with local access

Access to the GitHub Enterprise Server appliance shell and its containers is expected to include access to sensitive information and credentials that are required to operate local services.

### Bypassing source code de-obfuscation

GitHub Enterprise Server uses code obfuscation to discourage the modification of the application. We are aware of de-obfuscation techniques that could be used to reveal source code or bypass license restrictions.

