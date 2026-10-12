# Dependabot

Canonical page: https://bounty.github.com/targets/dependabot

## Synopsis

Dependabot powers [Dependabot security updates](https://docs.github.com/en/code-security/concepts/supply-chain-security/dependabot-security-updates), which allow GitHub users to automatically update vulnerable dependencies. The core logic of Dependabot is [open-source](https://github.com/dependabot/dependabot-core) and an [overview of the architecture](https://github.com/dependabot/dependabot-core#architecture) is available.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Execution environment breakout attacks, providing access to private networked resources or other users' data
* Security issues in [`dependabot-core`](https://github.com/dependabot/dependabot-core)

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Arbitrary code execution in dependency update jobs

The dependency update jobs are designed to execute arbitrary code. Update jobs run in a sandbox designed to execute untrusted code and prevent access to private networked resources or other users' data. Escaping the sandbox to access private networked resources or other user's data is a vulnerability and may be eligible for reward.

### Showing code execution without showing the escape

This is the most common ineligible Dependabot report we receive. A manifest, lockfile, or build script that runs your code during an update job is doing exactly what the job is for. The finding starts at the sandbox boundary. Your report needs to show something concrete on the other side of it, such as reaching an internal host, reading another customer's data, or obtaining credentials that outlive the job. Proof that your code ran, that you can see the container filesystem, or that you have network access to the public internet is not a sandbox escape.

### What Dependabot does with the repository it runs against

Dependabot acts on the repository that enabled it, using permissions that repository granted. Opening pull requests, reading the dependency graph, and writing to a branch it created are intended. Reports that someone who can already push to the repository can influence a Dependabot run are ineligible.

### Vulnerabilities in the packages themselves

Findings in third party packages, or in advisories published about them, belong to those maintainers. Report them to the package owner or through the [GitHub Advisory Database](https://github.com/advisories). Reports that Dependabot did not alert on a given package, alerted late, or scored an advisory differently to another source are ineligible.

