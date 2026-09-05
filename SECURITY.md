# Security policy

This repository contains deployment configuration and documentation for a Crafty Controller / Minecraft setup. It must not contain live credentials, private keys, private runtime configuration, Minecraft worlds, or host-specific secrets.

## Reporting a security problem

Do not publish credentials, tokens, private keys, private host details, or exploit details in a public issue.

If GitHub private vulnerability reporting is enabled for this repository, use that mechanism. Otherwise, contact the repository owner privately through their GitHub profile before sharing sensitive details.

## If a secret is committed

Treat a committed secret as compromised even if the commit is quickly reverted.

1. Revoke or rotate the credential at its issuing service first.
2. Remove it from the current tree.
3. Remove it from Git history if necessary.
4. Check forks, caches, build logs and artifacts where applicable.
5. Review access logs for unexpected use.

Deleting a file in a later commit does not remove it from earlier Git history.

## Repository hygiene

The repository is designed around these rules:

- `.env` and host-specific overrides stay local;
- Crafty runtime data stays outside the Git working tree;
- private keys and common credential files are ignored;
- only required network ports are published;
- the Crafty administrative UI should be restricted to trusted access paths;
- image upgrades are deliberate and version-pinned;
- automated secret scanning runs on pushes and pull requests.

See [docs/PUBLIC-REPO-SAFETY.md](docs/PUBLIC-REPO-SAFETY.md) before changing repository visibility to public.
