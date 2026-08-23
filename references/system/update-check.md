# Update Check

Use this guide when `assets/skill-tool/skill-tool.exe` already exists and you need to decide whether to keep it or update it.

Read [versioning.md](versioning.md) for the canonical skill version and repositories, then read [skill-tool.md](skill-tool.md) for the runtime layout.

## Check Rule

- Do not update automatically.
- Gather the local version first.
- Compare it with the newest GitHub release.
- If the newest release is a pre-release, present that fact to the user and let them decide whether to use it.
- Do not trust a single GitHub HTML snapshot when it conflicts with other evidence or looks partially loaded.

## Local Check

1. Confirm that `assets/skill-tool/skill-tool.exe` exists.
2. Change into `assets/skill-tool/`.
3. Run `skill-tool.exe --version`.
4. Record the exact version string returned by the tool.

## Remote Check

Use a release cross-check flow. Prefer at least two independent signals before concluding that there are no releases or that a specific release is latest.

Recommended signals:

1. the repository releases page
2. the direct release tag page for the candidate tag
3. the GitHub releases API when available in the environment
4. the visible asset list or asset count

Treat the releases page as inconclusive, not authoritative, if it shows any of these symptoms:

- "There was an error while loading"
- missing asset details while still showing a tag
- contradictory states such as a tag being listed together with partial-loading errors
- a stale-looking "There aren't any releases here" result that conflicts with direct tag pages or API data

Determine:

- the newest release tag
- whether it is a stable release or a pre-release
- which assets are attached
- whether the skill repository appears to have a newer version than the local value in `VERSION`

When the page is inconsistent:

- say that the HTML page snapshot is unreliable
- cross-check with the releases API or direct tag URLs before making a claim
- only tell the user "no releases" after those cross-checks also agree

## Real Failure Mode To Avoid

The GitHub releases page can simultaneously show valid releases and partial-loading errors. For example, on Sunday, August 23, 2026, the `Sukiet/WxArticle-Skill-Toolkit` page listed `a0.2` as Latest and `a0.1` as a Pre-release while also showing repeated "There was an error while loading" blocks. In that state, do not conclude that releases are missing just because one page state looks empty or broken.

## Decision Rule

- If no newer accepted release exists, keep the installed binary.
- If a newer stable release exists, explain the version difference and ask whether to update.
- If the newest release is a pre-release, tell the user the exact tag and ask whether to compare against or update to that pre-release.
- If the skill repository appears newer than the local `VERSION` value, tell the user the exact local version string from `VERSION` and that the repository may contain newer guidance.

## Update Steps

If the user approves the update:

1. Download the chosen release assets.
2. Replace `assets/skill-tool/skill-tool.exe` with the new binary.
3. If the chosen release provides a default environment file and the user wants it refreshed, replace `assets/skill-tool/.env`.
4. Run `skill-tool.exe --version` again from `assets/skill-tool/`.
5. Report the final installed version and whether it came from a stable release or a user-approved pre-release.

## Reporting Rule

When explaining your conclusion to the user:

- mention which release signals you checked
- state the exact tag you believe is latest
- state whether it is stable or pre-release
- note any page inconsistency if one existed
- avoid presenting a guessed conclusion as a verified fact
