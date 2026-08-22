---
name: wechat-article-writer
description: Draft and prepare WeChat article projects from user-provided content materials, template materials, and authoring constraints. Use when Codex needs to turn documents, images, prompts, template examples, or article instructions into a managed WeChat article workspace with `metadata.json`, `article.html`, and `images/`, while using `skill-tool` for project initialization, work-directory lookup, template retrieval, image compression, upload, and preview, and while checking GitHub releases for approved installation or updates when the local tool is missing or outdated.
---

# WeChat Article Writer

## Overview

Use this skill to produce a complete WeChat article project, not just a loose HTML draft. Treat the user's request as a combination of source content, template guidance, and non-negotiable constraints, then write the final article into the managed project created by the bundled CLI.

Follow the workflow in [references/workflow.md](references/workflow.md). Read the other references only when their topic is relevant:

- Read [references/input-contract.md](references/input-contract.md) when you need to normalize the user's delivery materials.
- Read [references/authoring-rules.md](references/authoring-rules.md) when deciding what may be rewritten, compressed, or kept unchanged.
- Read [references/skill-tool-cli.md](references/skill-tool-cli.md) before using the bundled CLI.
- Read [references/install.md](references/install.md) when `skill-tool.exe` is missing and the user may approve installation.
- Read [references/update-check.md](references/update-check.md) when checking the local version against GitHub releases.
- Read [references/deliverables.md](references/deliverables.md) before final handoff, upload, or preview.

## Required Workflow

1. Check whether `assets/skill-tool/skill-tool.exe` already exists.
2. If it is missing, read [references/install.md](references/install.md), explain the situation, and get user approval before installing from GitHub Releases.
3. If it exists, read [references/update-check.md](references/update-check.md), run `skill-tool.exe --version`, and compare it with the newest GitHub release.
4. If the newest release is a pre-release, tell the user the exact tag and ask whether they want to use it before installing or updating.
5. Confirm the article workspace location before starting content production.
6. If `assets/skill-tool/.env` already contains `WX_ARTICLE_REPO_DIR`, do not silently trust it. Tell the user the current path and ask whether to keep it or replace it.
7. If the repo path is missing or the user wants a different path, update `assets/skill-tool/.env` before running `init`.
8. Run `assets/skill-tool/skill-tool.exe` from `assets/skill-tool/` so the local `.env` is resolved correctly, then remember the returned `article_uuid`.
9. Ask whether the user wants to use a template. Do not choose or fetch one without user confirmation.
10. If a template is selected, fetch it first and study `example.html` plus `metadata.example.json` before drafting the formal article.
11. Write the formal outputs into `metadata.json`, `article.html`, and `images/`.
12. If you later need to re-locate an existing article project from its `article_uuid`, use `work-dir` before editing files in that project.
13. After each completed modification round that changes article HTML or article images, immediately run `upload`.
14. After each successful upload, immediately run `preview` and show the generated QR code to the user or client.

## Operating Rules

- Treat `article.html` as the canonical final content file inside the managed project, even if user examples mention names like `output.local.html` or `output.html`.
- Preserve template structure when the user says the template is mandatory. Do not remove components, alter outer wrappers, or change spacing rules unless the user explicitly allows it.
- Extract and place article images inside the project `images/` directory. Keep non-content template images unchanged unless the user explicitly asks to replace them.
- Use local file references while drafting if the template or workflow expects them. Only switch to remote image URLs when the user explicitly asks for the publish-ready version.
- Never improvise missing factual content. If the source materials do not support a claim, either omit it or flag the gap.
- Do not choose a template on the user's behalf.
- Do not install or update `skill-tool` until the user has explicitly approved the action.
- Do not treat a GitHub pre-release as automatically acceptable; surface it to the user and let them decide.
- Treat every completed HTML or article-image edit as requiring an immediate `upload` followed by `preview`.
- After `preview`, present the QR code to the user or client whenever the environment can display it.

## Bundled Resources

- `references/install.md`
  Install `skill-tool` from GitHub Releases after user approval.
- `references/update-check.md`
  Check the local `skill-tool` version against GitHub Releases and handle pre-releases carefully.
- `assets/skill-tool/`
  Runtime install location created only when the user approves installation.

## Final Handoff

When finishing, report:

- the article workspace path
- the `article_uuid`
- whether a template was used
- which files were updated
- whether upload or preview has already happened
