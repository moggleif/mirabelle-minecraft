# Public repository safety

A public repository should contain reusable configuration and documentation, not private deployment state.

## Never commit secrets

Do not commit:

- `.env` files with real values
- passwords
- API tokens
- private keys
- certificates containing private keys
- Crafty credentials
- backup archives
- live Minecraft server data
- private infrastructure configuration that does not need to be public

The repository's `.gitignore` blocks common local and runtime files, but `.gitignore` is only a safety net. Review every change before committing it.

## Treat Git history as public

Deleting a secret from the current branch does not remove it from previous commits.

If a real credential is committed:

1. Revoke or rotate it immediately.
2. Remove it from the repository.
3. Decide whether history rewriting is required.
4. Assume the exposed value may already have been copied.

See the repository [security policy](../../SECURITY.md) for the incident-handling expectations.

## Secret scanning

The repository runs Gitleaks over Git history on pushes and pull requests.

A successful scan reduces the chance of accidentally publishing recognized secret formats, but it cannot prove that every piece of private information is absent.

Human review still matters.

## Keep runtime data outside Git

Crafty runtime state and Minecraft worlds belong in persistent storage outside the repository working tree.

The Git repository should contain the deployment definition. Backups should contain the game state.

This separation also makes it possible to publish the repository without publishing player/world data.

## Use examples for deployment-specific values

Public configuration should use examples, placeholders or environment variables instead of embedding real deployment details.

For example:

```text
<repository-url>
<repository-directory>
```

Use `.env.example` to document required environment variables. Keep the real `.env` local to each deployment.

## Review public-facing documentation

Before merging documentation, check for information that may be technically harmless but unnecessarily specific to a private installation, including:

- private hostnames
- internal IP addresses
- personal email addresses
- usernames that identify private users
- filesystem paths that expose unnecessary personal details
- screenshots containing credentials or identifying data

Generic paths such as `/srv/crafty` in examples are acceptable when they are clearly illustrative and contain no private data.

## GitHub Actions security

Keep workflow permissions minimal. This repository's read-only validation workflows normally need only:

```yaml
permissions:
  contents: read
```

Pin third-party GitHub Actions to an exact commit SHA so a moving tag cannot silently change the code executed by the workflow.

Dependabot can propose updates to pinned Actions. Review those pull requests like any other dependency update.

## Pull request checklist

Before merging a change to a public repository, verify:

- no real secrets or credentials are present
- no runtime data is included
- `.env` remains untracked
- examples are generic
- documentation does not leak unnecessary private infrastructure details
- secret scanning passes
- Markdown/YAML/workflow/Compose checks pass where applicable
- the diff contains only the intended change

## If uncertain

If information is not necessary for someone to understand, deploy or operate the reusable project, leave it out of the public repository.
