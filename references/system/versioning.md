# Versioning

Use this guide when you need the current skill version, the canonical repositories, or a stable place to compare local guidance against remote updates.

Read the root [VERSION](../../VERSION) file first. It is the single source of truth for the local skill version.

## Current Skill Version Source

- local version source: `VERSION`
- current local version at the time this file was updated: `a0.1`

## Canonical Repositories

- skill repository: `https://github.com/Sukiet/WxArticle-Skill.git`
- skill-tool repository: `https://github.com/Sukiet/WxArticle-Skill-Toolkit.git`
- article injector repository: `https://github.com/Sukiet/WxArticle-Injector`
- skill-tool releases: `https://github.com/Sukiet/WxArticle-Skill-Toolkit/releases`

## Usage Rule

- Treat the root `VERSION` file as the canonical version source for the local skill package.
- Treat the repository links in this file as the canonical remote metadata for the skill, tool, and article injection plugin.
- Keep version and repository information under `references/system/`, not in the business-writing references.
- If you suspect the skill instructions are stale, compare the value in `VERSION` with the latest state in the skill repository before assuming the local package is current.
- If you suspect the bundled tool is stale, use the skill-tool repository and its releases page together with [update-check.md](update-check.md).
- If the GitHub releases page looks stale, empty, or partially broken, treat that as an unreliable signal and use the cross-check workflow in [update-check.md](update-check.md).

## Read Next

- Read [skill-tool.md](skill-tool.md) for runtime layout and config handling.
- Read [update-check.md](update-check.md) for installed tool version comparison.
