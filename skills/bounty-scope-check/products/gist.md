# GitHub Gist

Canonical page: https://bounty.github.com/targets/gist

## Synopsis

[GitHub Gist](https://gist.github.com) is our service for sharing snippets of code or other text content. Gist is built on Ruby on Rails and leverages a number of Open Source technologies.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* GitHub Gist features [exposed via git](https://help.github.com/articles/forking-and-cloning-gists/)

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Secret gists are accessible via URL without authentication

If you share the URL of a secret gist, anyone with access to the URL will be able to see it without authentication. This is an [intentional feature](https://help.github.com/articles/about-gists/#secret-gists). Secret gists aren't private. If you send the URL of a secret gist to a friend, they'll be able to see it. However, if someone you don't know discovers the URL, they'll also be able to see your gist. If you need to keep your code away from prying eyes, you may want to create a private repository instead.

### Gist content rendered on githubusercontent.com

Raw gist files and user uploaded images are served from `githubusercontent.com` rather than `github.com` precisely so that active content cannot reach your GitHub session. Scripting that executes on that domain, including in an SVG, has no access to `github.com` cookies. See [the `githubusercontent.com` page](https://bounty.github.com/targets/githubusercontent-com.html) for what is and is not eligible there.

### Links and redirects in gist content

A gist can contain any text, including links to sites the author controls. Reports that a link in a gist leads somewhere hostile, or that a URL shortener obscures its destination, are ineligible. The same applies to the interstitial we show when leaving GitHub: it is a warning, not a security boundary.

### Forks, revisions, and deletion

Gist history is kept in Git, so a revision that was once public may remain reachable through the Git interface or through a fork after the gist is edited or deleted. Treat anything published in a gist as published. If you committed a secret to a gist, rotate it.

