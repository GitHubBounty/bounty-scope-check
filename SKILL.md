---
name: bounty-scope-check
description: Help researchers develop bounty-worthy GitHub security findings, recognize when an observation is not bounty-worthy, and prepare strong HackerOne reports by checking scope, product focus areas, known-ineligible categories, demonstrated impact, and missing evidence.
license: See https://bounty.github.com/rules
compatibility: Works in any agent that supports the Agent Skills format. Network access to https://bounty.github.com is optional when the reference files are present locally; it is used to check whether this copy is current and to fetch any reference that is missing.
metadata:
  source: https://bounty.github.com
  built_on: "2026-10-02"
---

# GitHub Bug Bounty scope check

Helps researchers turn promising observations into bounty-worthy GitHub security
findings and concise, well-supported HackerOne reports. It checks published scope and
eligibility rules, identifies the strongest impact the evidence supports, and
recommends the next safe test that would make the finding more valuable.

The goal is not merely to reject weak reports. Help researchers spend their time on
findings that cross a real security boundary, prove the greatest legitimate impact,
and have the best chance of earning a bounty. Be equally clear when an observation is
not bounty-worthy so the researcher can stop or redirect the work instead of submitting
a report that does not meet the program's criteria. Never exaggerate severity or
substitute a theoretical attack for evidence.

This assessment is guidance based on the published program documentation and the
evidence the researcher provides. It is not pre-approval or a guarantee of eligibility,
severity, remediation, or reward. GitHub makes the final decision, and a valid finding
may receive no bounty if it is already known or duplicates an earlier report.

Content is generated from https://bounty.github.com. Generated on **2026-10-02**.

Resolve every referenced file path relative to the directory containing this
`SKILL.md` and prefer the local copy. If a referenced file is unavailable locally,
fetch the same relative path from https://bounty.github.com/scope-check/.

## Before you start

Fetch https://bounty.github.com/scope-check/index.json and compare its `built_on` value with the local
`built_on` above. If the published value is newer, say so first and tell the researcher
to update their copy, because scope rules change and a stale copy can be wrong. Name
the update command only for the tool they actually installed with, such as
`gh skill update` for the GitHub CLI; otherwise tell them to pull the latest copy from
https://github.com/GitHubBounty/bounty-scope-check rather than naming a command that may not apply. If the
request is blocked by network access, permissions, or a sandbox, continue with the
local files and state that freshness could not be verified. Do not warn merely because
the local copy is a certain number of days old.

## How to run the check

Work through all seven steps. Do not stop early at the first negative signal, because a
researcher needs the full picture to decide whether to keep investigating.

1. **Identify the product.** Match the finding to a product in the directory below and
   read that file. If no product matches, say so explicitly and continue using only the
   program-wide references. Do not guess which product applies. A matching product page
   establishes that the product is in scope.
2. **Check scope.** Read `reference/scope-and-domains.md`. Use it to verify the affected
   domain and its exclusions, and to identify standalone products without a product page.
   A GitHub-owned domain not listed there is out of scope. A product is out of scope only
   when it has neither a matching product page nor an entry in that reference.
3. **Check research safety.** Read `reference/research-safety.md` before proposing or
   performing another test. Its ownership, traffic, denial-of-service, and PII limits are
   mandatory. If the local reference is unavailable and the published copy cannot be
   fetched, do not recommend a next test.
4. **Check program-wide exclusions.** Read `reference/program-wide-ineligible.md`.
   These apply to every product and override product-level scope.
5. **Check the product page** for focus areas, out-of-scope items, and known ineligible
   submissions.
6. **Assess the evidence** using `reference/report-quality.md`.
7. **Develop the finding.** Identify the highest-impact claim already demonstrated and
   the next safe, permitted test most likely to prove a stronger security boundary
   crossing. If there is no credible path to a bounty-worthy finding, say so and
   explain why. Do not suggest testing against accounts, repositories, or
   organizations the researcher does not own.

## How to report your conclusion

Give a verdict of **Likely eligible**, **Likely defense in depth**, **Likely
ineligible**, or **Unclear**, then provide:

1. **Why:** the exact scope and policy reasoning.
2. **Demonstrated impact:** the strongest claim the current evidence supports.
3. **Recommendation:** choose exactly one: **Meets the documented submission
   criteria**, **Keep investigating**, or **Stop—this is not bounty-worthy**. Give the
   shortest useful reason.
4. **Best next test:** when recommending further investigation, give one concrete,
   safe test that would most improve eligibility or severity. Do not invent a test
   when no credible path remains.
5. **Report-ready outline:** include this only when recommending **Meets the documented
   submission criteria**. Provide a two-to-four-sentence summary, concise numbered
   reproduction steps with the evidence to attach, and a two-to-four-sentence impact
   statement. Do not draft a HackerOne report for an ineligible observation or write
   claims the evidence does not support.

Use **Likely defense in depth** only when the evidence establishes all of the following:
the finding is in scope, the behavior is reproducible, a specific security control
GitHub intended to enforce actually fails, and an independent protection prevents
demonstrated user impact. Identify both the failed control and the protection that
limits impact. See the defense in depth tier in
`reference/severity-and-rewards.md`.

Do not classify a product bug, unexpected behavior, unnecessary exposure, missing
optional hardening, or best-practice gap as defense in depth unless the report
demonstrates failure of an intended security control. These findings are not promoted
to a security tier merely because they are interesting or have a theoretical security
angle.

Follow these rules, which matter more than reaching a confident answer:

- **Only say a finding is ineligible when something in the documentation actually says
  so.** Quote the specific rule. Absence of a rule is not a rule.
- **When the documentation does not address the finding, say "the published guidance
  does not cover this" and treat the verdict as Unclear.** This is a useful answer. It
  identifies a genuine gap rather than inventing a policy.
- **Do not use defense in depth as a polite way of saying ineligible.** If a rule says
  the finding is ineligible, say ineligible and quote the rule. If the evidence does
  not establish failure of an intended security control, do not call it defense in
  depth. State what evidence would be required to cross that line.
- **Do not treat every technical observation as a bounty finding.** When the behavior
  is working as designed, a product-quality bug, abuse, an upstream issue, or lacks a
  demonstrated security-boundary crossing with no credible path to one, recommend
  stopping and name the appropriate alternative channel where the documentation
  provides one.
- **Distinguish normal product interaction from following attacker instructions.**
  Viewing a pull request, cloning or opening a repository, checking out a branch, and
  reviewing a contribution neither automatically qualifies nor disqualifies a report.
  Evaluate the product's security model, prompts, expected behavior, what the action
  inherently authorizes, and whether the product crosses a security boundary beyond
  that authorization. Pasting an attacker's command, running their script, changing a
  security setting, granting permissions, or overriding a warning does not establish
  a product vulnerability.
- Keep severity assessment grounded in demonstrated impact, not claimed impact. Do not
  anchor the assessment toward either a high or low tier before evaluating the evidence.
- Help the researcher maximize a legitimate reward by proving impact, not by adding
  verbosity, speculative chains, or inflated severity labels.
- State any unresolved assumption or missing evidence that could change the verdict.
  The skill cannot confirm whether GitHub already knows about the issue or whether
  another researcher submitted it first.
- Do not speculate about reward amounts.

Close by listing any point where the published guidance was silent, ambiguous, or
appeared to contradict itself, so it can be improved.

## Product directory

| Product | File |
|---|---|
| GitHub CSP | `products/csp.md` |
| Dependabot | `products/dependabot.md` |
| GitHub Gist | `products/gist.md` |
| GitHub Actions | `products/github-actions.md` |
| GitHub API | `products/github-api.md` |
| GitHub CLI | `products/github-cli.md` |
| GitHub Codespaces | `products/github-codespaces.md` |
| GitHub Copilot App | `products/github-copilot-desktop.md` |
| GitHub Copilot | `products/github-copilot.md` |
| GitHub Credentials | `products/github-credentials.md` |
| GitHub Desktop | `products/github-desktop.md` |
| GitHub Education | `products/github-education.md` |
| GitHub Enterprise Cloud | `products/github-enterprise-cloud.md` |
| GitHub Enterprise Server | `products/github-enterprise-server.md` |
| GitHub Mobile | `products/github-for-mobile.md` |
| *.github.net | `products/github-net.md` |
| GitHub Pages | `products/github-pages.md` |
| GitHub.com | `products/github.md` |
| *.githubapp.com | `products/githubapp-com.md` |
| *.githubusercontent.com | `products/githubusercontent-com.md` |
| npm CLI | `products/npm-cli.md` |
| npm Registry | `products/npm-registry.md` |

## Program-wide references

| Topic | File |
|---|---|
| In-scope products, domains, and excluded subdomains | `reference/scope-and-domains.md` |
| Ineligible across all products | `reference/program-wide-ineligible.md` |
| Research safety and rules of engagement | `reference/research-safety.md` |
| Severity and reward guidance | `reference/severity-and-rewards.md` |
| What a report needs to contain | `reference/report-quality.md` |

Full program rules, including the research restrictions and legal safe harbor, are at
https://bounty.github.com/rules. Submissions go to https://hackerone.com/github.
