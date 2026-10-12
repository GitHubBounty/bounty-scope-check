# GitHub Actions

Canonical page: https://bounty.github.com/targets/github-actions

## Synopsis

[GitHub Actions](https://github.com/features/actions) allows users to build, test, and deploy code right from GitHub. Action workflows are [configured](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/configuring-workflows) directly in the repository. Self-hosted runners [are available](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/hosting-your-own-runners) for users who require custom hardware configuration or operating systems not offered by GitHub-hosted runners.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Each repository in GitHub Actions is isolated from one another. Each job runs in a tenant which only contains resources for that single repository. It should not be possible to access resources from another repository's job.

* GitHub Actions have a [GitHub token](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/authenticating-with-the-github_token) available to them. This token is scoped to the repository from which the workflow is run. This token should not be able to access private content outside of that repository or [beyond the permissions listed in the documentation](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/authenticating-with-the-github_token#permissions-for-the-github_token).

* GitHub Actions provides a mechanism for GitHub.com to [store secrets](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets) associated with a repository. Upon invocation of a workflow, the secrets are fetched, decrypted, then made accessible to each [workflow run](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/core-concepts-for-github-actions#workflow-run).

* GitHub Apps and OAuth apps should not be able to edit the [workflow file](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/core-concepts-for-github-actions#workflow-file) in the repository. If an attacker is able to modify the workflow file then they gain access to secrets stored in the repository. This could allow an attacker to escalate their privileges if the application performing the editing has less permissions than the GitHub token accessible within the runtime environment.

* Official actions in the [`actions` organization](https://github.com/actions)

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Steps within a job are not security boundaries

A workflow job is a single trust domain. Any step that can run code in a job can already read the job's token, the secrets passed to that job, the workspace, the environment, and the runner's filesystem, and can influence every later step in the same job. Writing to `GITHUB_ENV` or `GITHUB_PATH`, setting a library preload variable, or altering a cache that a later step restores are all ways of doing something the step could already do directly.

Reports that move between steps of the same job are therefore ineligible. To be eligible, show the boundary around the job failing: reaching another repository, another job's secrets, another customer's runner, or job-scoped credentials that remain valid beyond their documented lifetime.

### Artifact upload and download paths

The upload and download artifact actions package and unpack whatever paths the workflow points them at. The workflow author chooses those paths, and anyone who can change the workflow or run code in the job can already read the files being packaged. Filtering of hidden files is a convenience so that people do not ship `.git` by accident, not a control over what a workflow is permitted to include.

Reports that a workflow can be made to include a hidden file, follow a symlink in its own workspace, or write outside the extraction directory when the artifact is created and consumed within the same job are ineligible. To be eligible, show the artifact crossing a job or repository boundary, such as an artifact from an untrusted job overwriting files used by a more privileged job, one repository reaching another repository's artifacts, or an artifact becoming readable by someone who could not already read the repository.

### Code Execution in Actions

It is an intentional design decision to allow root access to the machines running actions to give users greater flexibility and ability to install software for their CI. The VMs that run Actions are not persisted / re-used, and are continually recycled. Additionally, each machine is on its own VNet and should not have network visibility into other user's running Actions.

Additionally, it's expected and known behavior that the metadata service is accessible and it should not present a security risk. 

If you are able to demonstrate that you can access information from other VMs in the network, that may be eligible for reward.

### Bypassing build log secret redaction

To prevent accidental disclosure of secrets, GitHub Actions includes a mechanism to sanitize any [encrypted secrets](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets) that appear in build logs. Our mechanism attempts to match any secrets in common encodings, such as plaintext, base64, etc. It is _not_ designed to prevent users intentionally disclosing secrets in non-standard encodings and is therefore ineligible for reward.

### General abuse or exhaustion of resources

Intentionally misusing CPU, memory or network limits of GitHub Actions is a known issue. We take abuse and spam seriously and have a dedicated team that tracks spammy users. Therefore, this is ineligible for reward.

### Availability of resources inside a workflow run

A GitHub Actions build will intentionally have access to many resources including, but not limited to:
  * a metadata service available at `http://169.254.169.254`
  * a job token used to report status back to GitHub.com
  * privileged access to the host VM

Access to these resources is expected and not eligible for a reward. However, if these primitives can be abused to access resources of other repositories or users then this may be eligible for reward.

### Access to build artifacts without user session

Downloading build artifacts requires `read` access to a repository. When a user with `read` access clicks the download button, they will be given a link containing a signed token that is no longer tied to the user session. This is expected behavior and ineligible for reward.

