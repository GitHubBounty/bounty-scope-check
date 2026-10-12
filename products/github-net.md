# *.github.net

Canonical page: https://bounty.github.com/targets/github-net

## Synopsis

Subdomains under `*.github.net` run services for our internal production network. Many of these services are not accessible from outside our internal network.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Authentication bypasses allowing access to `*.github.net` services.
* Subdomain takeovers under `*.github.net`.
* Server Side Request Forgery vulnerabilities allowing access to our internal network. You may use `ssrf-target.iad.github.net` to test out SSRF attacks.

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Internal IP addresses and hostnames in public DNS

Some public DNS records resolve to RFC 1918 or otherwise internal addresses. On its own this tells an attacker nothing they can act on, because they still cannot route to those hosts. These reports are ineligible unless you pair them with a working path to reach the address, such as a server side request forgery that we can reproduce.

### Vulnerabilities in out-of-scope subdomains

Not all subdomains are in-scope for rewards at this time and are therefore ineligible for rewards. A list of out-of-scope subdomains is available in our [scope](https://bounty.github.com/scope) section.

