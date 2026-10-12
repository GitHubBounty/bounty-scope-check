# npm CLI

Canonical page: https://bounty.github.com/targets/npm-cli

## Synopsis

[The npm CLI](https://docs.npmjs.com/cli/commands) is the command line client that allows developers to install and publish packages to npm registries.

## Focus areas

Findings of this kind are the ones the program most wants for this product.

- Remote Code Execution (RCE): Since the npm CLI is a shell tool that is run on a developer's machine, the bar for an RCE is higher than for other assets. We consider the following to be examples of unintended RCE:
  - Arbitrary script execution upon package install with the `--ignore-scripts` flag
  - Arbitrary code execution from a command that should not modify the package tree
- Authentication theft/disclosure, such as inappropriately sending authentication credentials intended for a given server to some other server 
- Credentials (from the `.npmrc` file) being leaked in logs
- Package integrity compromise, i.e., downloading something that does not match the integrity of `package-lock.json`
- Overwriting an executable that already exists with a globally installed package if `--force` has not been set

## Known ineligible submissions

These have been reported before and are not eligible. Check this list carefully.

### Project configuration in a repository you chose to run npm in

npm reads configuration from the directory you run it in, including the project `.npmrc`, and that file can change where npm looks for further configuration. If you cloned an attacker's repository and ran npm inside it, the project files are attacker-controlled content you chose to trust, in the same way the lifecycle scripts below are.

Reports that a project `.npmrc` overrides your user settings, redirects a registry, or suppresses a warning are ineligible. A report is eligible if npm does something that does not depend on you having chosen to work inside that project.

### Social engineering

Code execution requiring social engineering or unlikely user interaction is typically not eligible for rewards.

### Local access

Vulnerabilities which require local system access, such as local credential storage issues.

### Arbitrary code execution in commands that modify the package tree

By default, commands that modify the package tree, such as `npm install`, run the pre- and post-install scripts. If you would like to disable this, [you can set the `--ignore-scripts` flag](https://docs.npmjs.com/cli/using-npm/config#ignore-scripts). However, note that general code execution that is achieved when using the `--ignore-scripts` flag is considered out of scope. [As stated in the npm documentation](https://docs.npmjs.com/cli/using-npm/config#ignore-scripts), setting the `--ignore-scripts` flag to true means that "npm does not run scripts specified in package.json files." Any code execution that occurs when using the `--ignore-scripts` flag, other than bypassing the specific intended behavior by successfully executing a pre- or post-install script from a package.json file, is considered ineligible.

### Upstream dependencies

Vulnerabilities that are due to a vulnerability in an upstream dependency are out of scope and should instead be disclosed to the upstream maintainers. We may make exceptions for vulnerabilities that we deem to have a substantial impact; however, issues should still be directed to the maintainers of the upstream dependency first.

