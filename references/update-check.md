# Update Check

Use this guide when `assets/skill-tool/skill-tool.exe` already exists and you need to decide whether to keep it or update it.

## Check Rule

- Do not update automatically.
- Gather the local version first.
- Compare it with the newest GitHub release.
- If the newest release is a pre-release, present that fact to the user and let them decide whether to use it.

## Local Check

1. Confirm that `assets/skill-tool/skill-tool.exe` exists.
2. Change into `assets/skill-tool/`.
3. Run `skill-tool.exe --version`.
4. Record the exact version string returned by the tool.

## Remote Check

Check the GitHub Releases page for:

- repository: `Sukiet/WxArticle-Skill-Toolkit`
- release page: `https://github.com/Sukiet/WxArticle-Skill-Toolkit/releases`

Determine:

- the newest release tag
- whether it is a stable release or a pre-release
- which assets are attached

## Decision Rule

- If no newer accepted release exists, keep the installed binary.
- If a newer stable release exists, explain the version difference and ask whether to update.
- If the newest release is a pre-release, tell the user the exact tag and ask whether to compare against or update to that pre-release.

## Update Steps

If the user approves the update:

1. Download the chosen release assets.
2. Replace `assets/skill-tool/skill-tool.exe` with the new binary.
3. If the chosen release provides a default environment file and the user wants it refreshed, replace `assets/skill-tool/.env`.
4. Run `skill-tool.exe --version` again from `assets/skill-tool/`.
5. Report the final installed version and whether it came from a stable release or a user-approved pre-release.

