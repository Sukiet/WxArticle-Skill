# Skill Tool Runtime

Use this guide when the task depends on the `skill-tool` runtime, its repository, or maintenance metadata.

Read [versioning.md](versioning.md) first when you need the canonical skill version or tool repository links.

## Purpose

Keep runtime and maintenance information separate from article-writing business rules. This file is the entrypoint for:

- where `skill-tool.exe` lives inside the skill
- where its `.env` lives
- which repository and GitHub release page it comes from
- which system references to read next
- where future skill or tool version metadata should live

## Runtime Layout

The packaged skill uses this runtime shape:

```text
assets/
  skill-tool/
    .env
    skill-tool.exe
```

Run `skill-tool.exe` from `assets/skill-tool/` so the local `.env` is resolved correctly.

## Config Variables

- `WX_ARTICLE_REPO_DIR`
  The root directory that will contain article projects.
- `WX_ARTICLE_HOST`
  The backend host used by the CLI.

Rule:

- `WX_ARTICLE_REPO_DIR` may be updated after user confirmation so the article workspace lives outside the skill package.
- Sensitive future config such as access tokens should not be rotated or replaced casually during ordinary drafting work.
- Do not inspect `skill-tool` source code just to infer the known required `.env` fields; use the documented keys in this skill unless release documentation explicitly changes them.

## Repository and Release Source

- skill repository: `https://github.com/Sukiet/WxArticle-Skill.git`
- skill-tool repository: `https://github.com/Sukiet/WxArticle-Skill-Toolkit.git`
- article injector repository: `https://github.com/Sukiet/WxArticle-Injector`
- skill-tool releases: `https://github.com/Sukiet/WxArticle-Skill-Toolkit/releases`

Keep repository links, release links, and future version metadata together under `references/system/` rather than scattering them across business writing docs.

## Article Injection Guidance

If the user approves the current version and asks how to inject the article into the WeChat backend, explain the workflow clearly:

- the user copies the `article_uuid` from the agent's reply
- the user logs into the WeChat official account backend
- the user waits for the injection plugin to recognize the page
- the user enters the `article_uuid` to inject the article

Explain plugin setup only when needed:

- the user needs a userscript manager such as Tampermonkey
- the user also needs the article injection plugin from `https://github.com/Sukiet/WxArticle-Injector`

Do not front-load this injection tutorial into every ordinary iteration handoff. The default handoff should only invite follow-up questions, and detailed injection help should appear only when the user asks or seems stuck.

## Read Next

- Read [versioning.md](versioning.md) when you need the current skill version.
- Read [install.md](install.md) when `skill-tool.exe` is missing.
- Read [update-check.md](update-check.md) when you need to compare the local tool with GitHub releases.
