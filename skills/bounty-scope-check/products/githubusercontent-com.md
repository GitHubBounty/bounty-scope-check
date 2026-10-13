# *.githubusercontent.com

Canonical page: https://bounty.github.com/targets/githubusercontent-com

## Synopsis

`*.githubusercontent.com` serves content that our users upload, including raw file contents, avatars, issue and pull request attachments, and rendered assets. It is a separate domain by design.

The important thing to understand before reporting here is that the domain separation **is** the security control. Content on `*.githubusercontent.com` is expected to be untrusted, and it is served away from `github.com` precisely so that untrusted content cannot reach `github.com` cookies or session state. Demonstrating that user-controlled content behaves in a user-controlled way on this domain is not a vulnerability on its own.

Reports are eligible when they show that separation failing, or that private content can be reached without proper authorisation.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Access to private repository content without a valid, unexpired signed token.
* Bypassing the Content Security Policy applied to user-uploaded content. A demonstrated CSP bypass may qualify as defense in depth when domain isolation prevents it from reaching sensitive state.
* Serving content on `*.githubusercontent.com` in a way that reaches `github.com` cookies or session state.
* Subdomain takeovers under `*.githubusercontent.com`.

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### User-content behavior without a CSP bypass

We serve user-uploaded content from `*.githubusercontent.com` specifically to isolate it from `github.com` and its cookies. Cross-site scripting, open redirects, and similar behaviour in an SVG or other uploaded file are contained by that separation. Demonstrating only that user-controlled content behaves in a user-controlled way is a known low risk and is ineligible.

We also apply a Content Security Policy as an intended security control. A report that reproducibly bypasses that policy may qualify as defense in depth even when the independent domain separation prevents user impact. A report that reaches `github.com`, its cookies, or its session state is eligible based on that demonstrated impact rather than as defense in depth.

### Tokens in raw file URLs

When you use the Raw button on a private file we generate a URL containing a cryptographically signed, time-limited token. That token authenticates access to that file for that user, and it works for anyone holding the URL until it expires. This is by design, so treat the URL as you would the file itself. Reports that a raw URL grants access without a session are ineligible unless you can show a token being forged, extended, or reused after expiry.

### Attachments on private issues and pull requests

Images and files attached to a private issue or pull request are served from a URL containing an identifier that is intended to be unguessable to someone without access to the repository. Treat the URL as you would the file itself. Reports that an attachment URL remains reachable to someone who was given it are ineligible. Reports that the identifier can actually be predicted, enumerated, or recovered from another endpoint are eligible, and we have rewarded them, so it is worth testing rather than assuming.

### Credentials found in user content

Credentials committed by our users are not GitHub credentials and are not in scope. See [GitHub Credentials](https://bounty.github.com/targets/github-credentials.html) for what we do consider in scope, and please report user-owned secrets to the repository owner instead.

