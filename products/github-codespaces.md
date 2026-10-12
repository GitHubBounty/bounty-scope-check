# GitHub Codespaces

Canonical page: https://bounty.github.com/targets/github-codespaces

## Synopsis

GitHub Codespaces provides cloud-hosted development environments that run in isolated containers on virtual machines.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Each codespace runs in an isolated container on a virtual machine. It should not be possible to escape the container to access other users' codespaces, the host infrastructure, or internal services.
* Unauthorized access to another user's running codespace, forwarded ports, or environment secrets.
* Codespaces provides mechanisms to store user [secrets](https://docs.github.com/en/codespaces/managing-your-codespaces/managing-your-account-specific-secrets-for-github-codespaces) and [organization secrets](https://docs.github.com/en/codespaces/managing-codespaces-for-your-organization/managing-development-environment-secrets-for-your-repository-or-organization). Secrets are scoped to specific repositories and should not leak across repository boundaries or through prebuild configurations.

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Devcontainer configuration and the codespace token

Opening a repository in a codespace runs that repository's devcontainer configuration, including its lifecycle commands. If you do not trust the repository, do not open it in a codespace. Code running there acts as you and can use the token available to that environment.

That token is scoped to the repository the codespace was created for. Reports showing a devcontainer running commands, reading the workspace, or using the codespace token against its own repository are ineligible. A report is eligible if you can show the token or the environment reaching a different repository, another user's codespace, or data outside that scope.

### API scopes are not a second set of permissions

A token scope controls which endpoints a token may call. It does not shrink the access the account already has. A token carrying the `codespaces` scope can therefore act on private repositories its owner can already reach, including creating a codespace for them, and that is the intended design rather than an escalation. Reports that a scope grants access the user already had are ineligible.

### Resource consumption within a user's own codespace

Reports about excessive CPU, memory, disk, or storage consumption within a user's own codespace are billing or quota concerns, not security vulnerabilities. This includes bypassing disk partition limitations within the codespace VM.

### Access to metadata services from within a codespace

Codespace VMs may have access to cloud metadata services (for example, 169.254.169.254). Network access to and retrieval of metadata from these services within the same codespace VM is expected behavior and not eligible for a reward.

Reports are eligible only if metadata service access can be used to cross tenant boundaries, access another user’s codespace, access GitHub internal infrastructure, or otherwise violate Codespaces isolation guarantees.

### Vulnerabilities in third-party software within a codespace

Codespaces run user-defined environments configured via [dev containers](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers). Vulnerabilities in third-party packages, Docker images, VS Code extensions, or other software, whether pre-installed or added by the user or their dev container configuration, are the responsibility of the upstream maintainer and not eligible for a reward. This includes known CVEs in pre-installed dependencies.

### Privileged access within a user's own codespace

A codespace will intentionally provide its user with elevated access including, but not limited to:
  * root access within the container
  * access to the Docker socket (`docker.sock`)
  * ability to mount host directories via Docker Compose
  * read access to VM-level resources such as `/proc`

This level of access within a user’s own codespace is expected by design and not eligible for a reward. However, if these capabilities can be used to access another user’s codespace, reach GitHub internal infrastructure, or otherwise cross the codespace’s VM isolation boundary, that would be in scope.

