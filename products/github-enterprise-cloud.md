# GitHub Enterprise Cloud

Canonical page: https://bounty.github.com/targets/github-enterprise-cloud

## Synopsis

GitHub Enterprise Cloud is the cloud-hosted version of GitHub Enterprise. It is designed for teams who want advanced authentication and permissions without managing infrastructure. More information about GitHub Enterprise Cloud is available at [https://github.com/enterprise](https://github.com/enterprise).

GitHub Enterprise Cloud with data residency is the cloud-hosted version of GitHub Enterprise where you can have more control over your data without needing to host your own platform. It offers you a flexibility to choose where your company's code and data are stored. More information is available at [https://docs.github.com/en/enterprise-cloud@latest/admin/data-residency/about-github-enterprise-cloud-with-data-residency](https://docs.github.com/en/enterprise-cloud@latest/admin/data-residency/about-github-enterprise-cloud-with-data-residency).

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Access to private repository, organization, or enterprise resources by an account that is not authorized to access them
* Bypasses of enterprise controls such as SAML enforcement, IP allow lists, or SSO-protected credentials
* Escalation from a lower enterprise or organization role to a higher one

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Access that a role is supposed to grant

Enterprise owners, organization owners, and repository administrators have broad access by design, including to private repositories, member data, audit logs, and billing. Custom repository roles grant whatever permissions the organization assigned to them. Reports that an account with one of these roles can see or do something within its own scope are working as designed. Before reporting, check the [permission tables in our documentation](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-user-access-to-your-organizations-repositories) and say which specific permission the account should not have had.

### Actions workflows behaving as configured

A user who can push to a branch can change the workflows that run from it, and workflows run with whatever permissions the repository and organization settings allow. Reports that a workflow can read secrets available to it, or that a maintainer can add a workflow step, are ineligible. Show a workflow reaching secrets or resources belonging to a repository or organization it should not.

### IP allow lists and network controls

IP allow lists restrict where requests may originate. They are not intended to hide the existence of an organization, block unauthenticated public content, or protect against a member who is inside the allowed range. Reports that public data is still public, or that an allowed address still works, are ineligible.

### Invitations, seats, and billing

Sending an invitation to an email address, a member consuming a seat, and usage counting against a billing plan are all intended behaviour. Reports about billing quantities without a demonstrated financial impact to GitHub or another customer are ineligible. See our position on [Copilot and consumption billing](https://bounty.github.com/ineligible).

### SSO redirects revealing that a resource exists

Enterprise owners can choose whether an unauthenticated request for an enterprise resource returns a 404 or redirects to single sign on. Where an administrator has enabled the redirect, it will reveal that the resource exists. That is a consequence of the setting they chose, so reports that the redirect distinguishes a real resource from a missing one are ineligible unless you can reach the private content itself.

### Repository visibility policies, forks and transfers

A policy that restricts repository visibility governs the actions it names, which is creating a repository and changing an existing repository's visibility. It is not a guarantee that no public repository can ever appear in the organization. Forking a public repository, transferring one in, and other routes that bring an existing repository along with its current visibility are governed by their own separate settings.

Reports that a visibility policy did not block a fork or a transfer are ineligible. Read the policy's own description first, and to be eligible show a member changing the visibility of a repository in a way the policy says it prevents.

