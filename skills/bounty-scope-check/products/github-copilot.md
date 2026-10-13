# GitHub Copilot

Canonical page: https://bounty.github.com/targets/github-copilot

## Synopsis

[GitHub Copilot](https://github.com/features/copilot) is an AI coding assistant that suggests code and entire functions in real-time, right from your editor.

[First-party Copilot Features](https://docs.github.com/en/copilot) available under `https://github.com/copilot` are in scope, including newly launched features that appear there.

[GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli) is in scope for this program. It gives you quick access to a powerful AI agent from your terminal and can help you complete development tasks more efficiently.

[Copilot coding agent](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent) is in scope. It can be assigned an issue or a pull request and works in a GitHub Actions environment scoped to that repository, opening a pull request for review when it is done. The boundary we care about is that environment: reports should show the agent reaching something outside the repository it was assigned to, or its changes landing without the review the repository requires.

[GitHub Copilot Enterprise](https://docs.github.com/en/copilot/github-copilot-enterprise/overview/about-github-copilot-enterprise) is a Copilot plan available for enterprises that use GitHub Enterprise Cloud.
- [Copilot Chat](https://docs.github.com/en/copilot/github-copilot-enterprise/copilot-chat-in-github/about-github-copilot-chat)
- [Copilot pull request summaries](https://docs.github.com/en/copilot/github-copilot-enterprise/copilot-pull-request-summaries/about-copilot-pull-request-summaries)
- [Copilot knowledge bases](https://docs.github.com/en/enterprise-cloud@latest/copilot/github-copilot-enterprise/copilot-chat-in-github/managing-copilot-knowledge-bases)

## Focus areas

Findings of this kind are the ones the program most wants for this product.

- Escalating to another user's session that you do not own and accessing their session content
- Bypassing Copilot’s proxy or mediation layer in a way that results in increased access or privilege
- Vulnerabilities that demonstrate a clear, material security impact to confidentiality, integrity, or availability within GitHub Copilot, including:
  - **Authorization vulnerabilities** (for example: privilege escalation, cross-tenant/cross-repository data access, or bypass of Copilot/org/enterprise policy controls)
  - **Unauthorized actions / integrity-impacting behavior** (for example: actions performed without expected user confirmation, or flows that defeat intended guardrails)
  - **Data exposure** (for example: access to private repository content or other protected GitHub data outside the reporter’s authorized access)
> **Note**: We are aware of prompt injection techniques. Reports that only demonstrate influence over Copilot output, without a broken authorization boundary or unauthorized action (e.g., authorization bypass, cross-tenant data exposure, or unauthorized actions), are generally not eligible.

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Vulnerabilities in GitHub Copilot Chat extension and Inline Suggestions in Visual Studio Code

The [GitHub Copilot Chat extension](https://code.visualstudio.com/docs/copilot/chat/getting-started-chat) and [Inline Suggestions from GitHub Copilot](https://code.visualstudio.com/docs/copilot/ai-powered-suggestions) in Visual Studio Code are features owned and maintained by Microsoft. Vulnerabilities affecting these features should be reported directly to Microsoft through their [Bug Bounty Program](https://www.microsoft.com/en-us/msrc/bounty).

### Prompt Injections

We are aware of prompt injection techniques (including indirect or “invisible” prompt injection via untrusted content such as issue/PR descriptions, comments, or repository files) that may attempt to influence Copilot output.
Reports that **only** demonstrate that Copilot’s output can be influenced or redirected by untrusted content are **not eligible** for a reward.
- Prompt injection reports **may be eligible** only when they demonstrate a concrete security impact such as:
  - **Privilege escalation** or **authorization/policy bypass**
  - **Cross-tenant / cross-repository data exposure**
  - **Unauthorized actions** occurring without required user confirmation or that bypass enforced authorization, policy, or safety controls.

### The security of code suggested by Copilot

GitHub Copilot is designed to generate the best code possible given the context it has access to, but it doesn’t test the code it suggests, so the code may not always work or even make sense. GitHub Copilot can only hold a very limited context, so it may not make use of helpful functions defined elsewhere in your project or even in the same file. It may also suggest old or deprecated uses of libraries and languages.

For suggested code, certain languages like Python, JavaScript, TypeScript, and Go might perform better than other programming languages. In addition, when converting comments written in non-English to code, there may be performance disparities when compared to English. 

Although Copilot suggestions are not part of the Bug Bounty program, you are welcome to report any vulnerable patterns you identify in code suggestions to copilot-safety@github.com. [Our blog has more information about our approach to securing code suggestions](https://github.blog/2023-02-14-github-copilot-now-has-a-better-ai-model-and-new-capabilities/).

### Tokens suggested by Copilot

Any strings suggested by Copilot that resemble tokens are not eligible.

### Prototype features

Any Copilot features that are not yet publicly accessible are considered out of scope.

### Copilot quota, billing, and usage limits

Premium request counts, quota resets, plan upgrades and downgrades, trial eligibility, and payment state are billing matters rather than security boundaries. Reports that you can obtain more Copilot usage than you paid for, reset a limit, or enrol yourself in a plan you are already able to enrol in are ineligible, and are handled as abuse through [support](https://support.github.com/request).

A report is eligible if the billing behaviour also crosses a security boundary, for example consuming another organization's entitlement, or reading another customer's usage or payment data.

Related reports we also close: enrolling an account you already control into a free tier, code in your own codespace or workspace using the token available to it to do the same, changing your own telemetry preference, and reading model names, versions, or policy metadata. None of these reach another customer's data.

### Changes you review and accept

Copilot proposes; you decide. When Copilot describes a change to your project, including to build files, configuration, or scripts, and you accept it or run the result, the outcome follows from your decision. Reports that untrusted content influenced a suggestion that you then approved are prompt injection, covered above.

To be eligible, show the change being applied or executed without the confirmation that step normally requires.

### GitHub MCP Server

The MCP server exposes GitHub data and actions to an AI client using your own credentials, so it can reach whatever you can reach. Tool annotations and descriptions are advisory metadata for the client, not an authorization control we enforce.

Reports that repository content, issues, or search results influence what a model does, or that a client chose to call a tool marked read-only, are prompt injection and are covered above. To be eligible, show the server itself returning data your token should not reach, or performing an action your token should not be able to perform.

### Off topic conversation

Any Copilot chat conversations that are off topic and not programming-related are not eligible.

### Copilot coding agent acting on a repository it was assigned to

When the coding agent is assigned an issue, it reads that repository and works in an environment scoped to it. Reports that the agent read the repository's code, issues, or workflow files, or that it ran the repository's own setup steps, describe the feature working. An eligible report shows the agent reaching a repository, secret, or network resource outside the one it was assigned to.

### Who can assign the coding agent

Anyone with the permission to assign issues in a repository can assign the agent, and the agent then works with that repository's access. That is the intended model. Reports that a collaborator can direct the agent, or that an issue title or body influences what the agent does within its own repository, are ineligible. Content the agent reads is untrusted input, and steering it is prompt injection, covered above.

### Agent output requires review

The agent opens pull requests for a human to review, and its branches are subject to the same branch protection and required review settings as any other contributor. Reports that the agent proposed insecure or incorrect code are ineligible for the same reasons as suggested code above. An eligible report shows the agent's changes reaching a protected branch without the review that branch requires.

