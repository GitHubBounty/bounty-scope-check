# GitHub CSP

Canonical page: https://bounty.github.com/targets/csp

## Synopsis

While content-injection vulnerabilities are already in-scope for our [GitHub.com bounty](https://bounty.github.com/targets/github.html), we also accept bounty reports for novel [CSP](https://developers.google.com/web/fundamentals/security/csp/) bypasses affecting GitHub.com, even if they do not include a content-injection vulnerability. Using an intercepting proxy or your browser's developer tools, experiment with injecting content into the DOM. See if you can execute arbitrary JavaScript or exfiltrate sensitive page contents such as CSRF tokens. Reports of other previously-unknown impacts from content-injection will also be considered.

You can find a discussion of known attacks and our attempts to mitigate them [here](https://github.blog/2016-04-12-githubs-csp-journey/). Attacks against CSP features not used on GitHub.com, such as script nonces, are not eligible for reward. Vulnerabilities resulting from injection in implausible locations, such as within an element that doesn't contain user-content, are not eligible for reward.

## Coverage gap

This product page does not currently define focus areas, out-of-scope items, or known ineligible submissions. Judge it against the program-wide rules in `reference/program-wide-ineligible.md` and `reference/scope-and-domains.md`, and state plainly that product-specific guidance is missing.

