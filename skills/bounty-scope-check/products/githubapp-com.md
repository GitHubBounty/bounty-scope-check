# *.githubapp.com

Canonical page: https://bounty.github.com/targets/githubapp-com

## Synopsis

Subdomains under `*.githubapp.com` provide a number of internal services to GitHub employees. These include our internal blog, helpdesk and bastion access to our internal network.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Authentication bypasses allowing access to `*.githubapp.com` services.
* Subdomain takeovers under `*.githubapp.com`.
* Server Side Request Forgery vulnerabilities allowing access to our internal network. You may use `ssrf-target.iad.github.net` to test out SSRF attacks.

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Vulnerabilities in out-of-scope subdomains

Not all subdomains are in-scope for rewards at this time and are therefore ineligible for rewards. A list of out-of-scope subdomains is available in our [scope](https://bounty.github.com/scope) section.

### Subdomain takeovers that cannot actually be taken over

A dangling DNS record is only eligible once you can show that you are able to claim the target and serve content from it. A CNAME pointing at a provider, a `NoSuchBucket` page, or a default landing page is not enough on its own. Include evidence that you registered the resource, and do not host anything beyond a harmless proof file.

### Third party services hosted on the domain

Some subdomains point at vendor services such as identity providers and support tooling. Findings in the vendor's own product should go to that vendor. We are interested in cases where the integration itself is broken, for example a misconfiguration that lets you reach GitHub data you should not have.

### Content that is meant to be public

Directory listings, static assets, health check endpoints, build metadata, and framework version banners on these hosts are ineligible on their own. Explain what an attacker gains from the disclosure.

