# GitHub Pages

Canonical page: https://bounty.github.com/targets/github-pages

## Synopsis

GitHub Pages is our static site hosting service designed to host your personal, organization, or project pages directly from a GitHub repository. It uses the [Jekyll](https://jekyllrb.com) static site generator and officially supported themes are developed in the [`pages-themes`](https://github.com/pages-themes) organization. GitHub Pages support [custom domains](https://help.github.com/articles/using-a-custom-domain-with-github-pages/) and can be secured with [HTTPS](https://help.github.com/articles/securing-your-github-pages-site-with-https/).

More information is available at [https://pages.github.com](https://pages.github.com)

## Focus areas

Findings of this kind are the ones the program most wants for this product.

* Escaping the isolation of the build process through a custom Jekyll theme or vulnerabilities in the command-line Git tools when cloning or checking out repositories
* Reading files outside the build's own boundary which discloses sensitive information, for example by misusing path traversal or symbolic links in a custom Jekyll theme

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Vulnerabilities in GitHub Pages hosted content

GitHub users are responsible for the content hosted on GitHub Pages sites. Any vulnerabilities in user content do not affect the security of GitHub.com or its users. We recommend that you report this issue to the owner of this GitHub Pages site.

### Subdomain Takeover

Subdomain takeovers on GitHub Pages are a known issue that does not present a significant security risk. We are aware of the risks associated with DNS records pointing to GitHub Pages without an intended repository being configured to use the domain. If you have had your domain taken over, please reach out to [Support](https://support.github.com/request) for help reclaiming it.

### Code execution during your own build

A Pages build runs the repository's own configuration and theme, so a user who can push to the repository can influence what the build does. That is the point of the feature. An eligible report shows a build reaching outside its own boundary: another repository's source, another customer's build, credentials belonging to GitHub, or the internal network. Show what you reached, not just that your code ran.

### Domain verification and custom domains

Custom domain verification proves that a domain owner intends to point at a particular account. It does not prevent anyone from setting a `CNAME` file in their own repository, and an unverified domain that nobody has claimed is not a vulnerability by itself.

