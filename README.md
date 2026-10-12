# bounty-scope-check

An agent skill that helps security researchers develop bounty-worthy GitHub
security findings and prepare strong HackerOne reports.

It checks a finding against the published scope and eligibility rules, identifies
the strongest impact the evidence actually supports, recommends the next safe test,
and — when the finding meets the documented submission criteria — drafts a
report-ready outline.

## Install

With the GitHub CLI, which is the path we support:

```
gh skill install GitHubBounty/bounty-scope-check
```

This is a standard [Agent Skills](https://agentskills.io) package, so other agents
can read it too. They have no install command for a GitHub repository, so clone it
into the directory they scan. Keep the directory named `bounty-scope-check`, because
the format requires the directory name to match the skill name.

Claude Code:

```
git clone https://github.com/GitHubBounty/bounty-scope-check.git \
  ~/.claude/skills/bounty-scope-check
```

Codex:

```
git clone https://github.com/GitHubBounty/bounty-scope-check.git \
  ~/.agents/skills/bounty-scope-check
```

Update a cloned copy with `git -C <that directory> pull`.

## What this is not

**This repository is a snapshot, not a source of truth.** It is generated from
<https://bounty.github.com> and may be out of date. Check the live site and the
program policy at <https://hackerone.com/github> before relying on anything here.

**Running this skill is not pre-approval.** A verdict from this skill is guidance
based on published documentation and the evidence you provide. It is not a
guarantee of eligibility, severity, remediation, or reward. GitHub makes the final
decision, and a valid finding may receive no bounty if it is already known or
duplicates an earlier report.

The skill checks whether your copy is current each time it runs. If it reports that
your copy is stale, update before relying on the result: `gh skill update` if you
installed with the GitHub CLI, or `git pull` in the directory you cloned into.

## Reporting a vulnerability

**This repository is not an in-scope bounty target.** Reports about this
repository, its contents, or its configuration are out of scope and will be
closed. In-scope products are listed at <https://bounty.github.com/targets>.

To report a vulnerability **in a GitHub product**, submit it to
<https://hackerone.com/github>. Issues are disabled here, and pull requests are
not an appropriate channel. See [SECURITY.md](SECURITY.md).

Full program rules are at <https://bounty.github.com/rules>.

## Contributions

Pull requests are not accepted — see [CONTRIBUTING.md](CONTRIBUTING.md). If
something here is wrong or out of date, email `bounty@github.com`.
