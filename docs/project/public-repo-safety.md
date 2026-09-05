# Public repository safety

This page is for whoever maintains the project's code, rather than for running Minecraft. Read it before making this repository public, or before pushing changes to it once it already is.

Making a repository public shares more than the files you can see right now. **Git history, commit metadata, branches, tags, issues, Actions logs and other repository metadata become visible too.** A password deleted last week is still sitting in last month's commit.

> **The short version:** never commit `.env`, passwords, keys, or anything that describes your actual home network. Use example values like `minecraft.example.net` and `192.0.2.10` in documentation.

## 1. Keep deployment-specific information local

The public repository should contain examples and reusable configuration, not a map of a real installation.

Do not commit:

- public or private IP addresses tied to a real deployment;
- private/admin DNS names;
- VPN configuration;
- router or firewall exports;
- SSH configuration containing real hosts;
- usernames when they reveal unnecessary personal information;
- screenshots containing addresses, account names, tokens or internal topology;
- Crafty runtime configuration;
- Minecraft worlds, player data or server logs;
- backup archives.

Use documentation placeholders such as:

```text
minecraft.example.net
192.0.2.10
<repository-url>
<host-address>
```

The documentation may describe an architecture without publishing the details of a specific installation.

## 2. Never commit credentials

Never commit:

- `.env`;
- passwords;
- API keys or tokens;
- SSH private keys;
- TLS private keys;
- keystores;
- Crafty's generated credentials;
- authentication cookies or session data.

`.gitignore` is a safety net, not a security boundary. Always inspect staged changes before committing:

```bash
git status
git diff --cached
```

## 3. Remember that Git keeps history

Removing a sensitive file in a later commit does **not** remove it from earlier commits.

Inspect repository history rather than only the current checkout:

```bash
git log --all --stat
git log -p --all
```

The repository also runs Gitleaks in GitHub Actions with full history checked out. Verify that the **Secret scan** workflow is green.

If a real secret has ever been committed, rotate/revoke the secret first. History rewriting is secondary; a secret should be treated as compromised once committed.

## 4. Check tracked and ignored files

Review exactly what Git is tracking:

```bash
git ls-files
```

Review ignored files too, so that an accidental force-add does not go unnoticed:

```bash
git status --ignored
```

Runtime directories should remain outside the working tree. If they are ever created inside it, the repository's `.gitignore` excludes the common Crafty runtime directory names.

## 5. Check commit identity

Public commits expose their commit metadata. If a personal email address should not be public, configure Git to use the GitHub-provided `noreply` address before making new commits.

Check existing history with:

```bash
git log --format='%h %an <%ae>' --all
```

Changing Git configuration only affects future commits. Removing an email address from existing commit history requires rewriting history.

## 6. Check names and privacy

Repository names, branch names, commit messages and documentation are public metadata too.

Decide deliberately whether names of people, households, schools, locations or projects should be associated with the public repository. This is a privacy decision even when it is not a technical security vulnerability.

## 7. Minimize exposed services

The Compose example publishes only the services needed for this setup:

- Crafty's HTTPS port;
- a small configurable Minecraft Java port range.

Do not add ports merely because an application can use them. Add Bedrock, map servers or other services only when they are actually required.

The Crafty administration interface should normally be restricted by a firewall, LAN/VPN policy or reverse-proxy access control. Publishing the source repository does not require publishing the administration interface.

## 8. Review third-party automation

GitHub Actions execute third-party code. This repository pins Actions to specific commit SHAs rather than floating branch or major-version references.

When updating an Action:

1. verify the upstream repository and release;
2. review the release notes;
3. update the pinned commit SHA;
4. keep a version comment next to the SHA;
5. review the resulting workflow run.

## 9. GitHub security settings

For a public repository, enable or verify GitHub's repository security features under **Settings → Advanced Security**, especially:

- secret scanning;
- push protection;
- Dependabot alerts where applicable.

GitHub provides secret scanning for public repositories. The repository-level Gitleaks workflow remains useful as an additional independent check.

## Public repository checklist

Verify all of the following:

- current files contain no deployment-specific secrets or unnecessary personal data;
- Git history has been reviewed;
- commit author email exposure is acceptable;
- `.env` and runtime data are not tracked;
- no real credentials have ever been committed, or any that were have been revoked;
- the Secret scan workflow passes;
- repository/branch/commit names are acceptable as public metadata;
- documentation uses examples rather than private infrastructure details;
- no Actions logs or artifacts contain sensitive data.

See the repository [security policy](https://github.com/moggleif/mirabelle-minecraft/blob/main/SECURITY.md) for handling security problems and accidentally committed secrets.

---

**Back to:** [Start here](../index.md)
