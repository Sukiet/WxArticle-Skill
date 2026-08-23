# Install

Use this guide when `assets/skill-tool/skill-tool.exe` is missing.

Read [versioning.md](versioning.md) for the canonical skill version and repository links, then read [skill-tool.md](skill-tool.md) for the runtime layout.
Read [update-check.md](update-check.md) if the GitHub releases page looks incomplete, contradictory, or partially loaded.

## Install Rule

- Do not install automatically.
- Explain to the user that the local tool is missing.
- Get explicit approval before downloading or writing any files.

## Pre-release Rule

- If the newest release is marked as a pre-release, tell the user the exact tag.
- Ask whether they want to install from that pre-release.
- Only continue if the user explicitly accepts it.

## Install Steps

1. Identify the newest accepted release using the cross-check rules in [update-check.md](update-check.md).
2. Inspect the release assets.
3. Download `skill-tool.exe`.
4. Also download any release asset that should serve as the default environment file, if such an asset exists.
5. Create `assets/skill-tool/` if it does not already exist.
6. Place `skill-tool.exe` at `assets/skill-tool/skill-tool.exe`.
7. Place the default environment file at `assets/skill-tool/.env` if the release provides one.
8. If the release does not provide a default environment file, create `.env` manually with the required keys:
   `WX_ARTICLE_REPO_DIR` and `WX_ARTICLE_HOST`.
9. Run `skill-tool.exe --version` from `assets/skill-tool/` to verify the install.
10. Report the installed version and whether it came from a stable release or a user-approved pre-release.

Do not inspect `skill-tool` source code to guess required `.env` fields. Treat this document as the authority for the known required keys unless the published release documentation changes.

## Current Known Asset Pattern

As of Sunday, August 23, 2026, observed releases include:

- `a0.2` as a stable release
- `a0.1` as a pre-release

Observed assets include at least:

- `skill-tool.exe`
- `QUICKSTART.md`

Do not assume this list, release order, or asset count is permanent. Always inspect the actual latest release before acting, and cross-check if the GitHub page looks inconsistent.
