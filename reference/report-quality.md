# What a report needs to contain

Most rejected reports fail on evidence rather than on scope. A finding can be real, in scope, and still be closed because the report does not show it happening. Keep the report concise and organize it into the three sections below. Long background explanations, repeated claims, speculative attack chains, and generic remediation advice make the actual finding harder to validate.

## Summary or description

In two to four sentences, identify the affected product or component, describe the vulnerability, and state the security boundary that is crossed. This should tell us what happened without requiring a long introduction or general explanation of the vulnerability class.

## Steps to reproduce

Provide concise, numbered steps that start from a clean state and demonstrate a working proof of concept. Include every required account, permission, configuration value, request, response, command, and user action. Attach screenshots, HTTP requests and responses, terminal output, or a short video where they help prove the result. A video is supporting evidence and does not replace written reproduction steps.

## Impact statement

In two to four sentences, state what the demonstrated attack allows an attacker to gain, which user or resource is affected, and the access or interaction the attacker needs before the attack begins. Describe the impact shown by the proof of concept, not a larger theoretical outcome. "This could lead to account takeover" is not an impact statement unless the report demonstrates the takeover.

## State prerequisites honestly

Viewing an issue or pull request, cloning or opening a repository, checking out a branch, and reviewing a contribution do not automatically make a finding eligible or ineligible. Context matters: the report must show the product crossing a security boundary in a way the action does not inherently authorize, taking account of the product's security model, prompts, and expected behavior. Copying and pasting an attacker's command, running their script, changing a security setting, granting permissions, or overriding a warning are attacker instructions, not product behavior. Do not hide or minimize a required victim action.

## Your own verification

Scanner output and AI-assisted analysis are acceptable starting points, but you are responsible for confirming the finding is real and reproducible before submitting. Unverified automated output is the most common source of invalid reports.

## Things that reliably do not qualify

These come up often enough to call out. They are closed on sight unless the report demonstrates something beyond the finding itself:

- Missing security headers with no demonstrated attack
- Product bugs, unexpected behavior, unnecessary exposure, or best-practice gaps that do not demonstrate the failure of an intended security control
- Self-XSS, or attacks needing implausible social engineering
- Attacks that require the victim to paste a command, run attacker-supplied code, change a security setting, grant permissions, or override a warning
- Theoretical access-control issues with no proof of accessing anything sensitive
- Disclosure of information that is already public or is not sensitive
- Findings on out-of-scope, deprecated, or test endpoints
