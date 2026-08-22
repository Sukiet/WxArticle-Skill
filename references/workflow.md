# Workflow

## Step 1. Confirm the Workspace Directory

Before article creation, inspect whether `assets/skill-tool/skill-tool.exe` exists.

- If it is missing, read [install.md](install.md), explain the issue, and only install after user approval.
- If it exists, read [update-check.md](update-check.md), run `skill-tool.exe --version`, and compare it with the newest GitHub release.
- If the newest release is a pre-release, tell the user the exact tag and ask whether to use it.

Then inspect `assets/skill-tool/.env`.

- If `WX_ARTICLE_REPO_DIR` is empty, ask the user to choose a workspace directory.
- If it already has a value, tell the user what it is and ask whether to keep it.
- If the user changes it, update `.env` first.

The article workspace should live outside the skill package so generated projects, uploaded images, and cache files do not pollute the skill source.

## Step 2. Initialize the Managed Project

Change into `assets/skill-tool/`, run `skill-tool.exe init`, and store the returned `article_uuid`.

Do not lose this id during the rest of the conversation.

If you return to an existing article later and only know its `article_uuid`, run `skill-tool.exe work-dir -a {article_uuid}` first so you can target the right local project files.

## Step 3. Decide Whether a Template Is Needed

- Ask the user whether to use a template.
- If yes, run `templates-list`.
- After the user chooses a template, run `fetch-template`.

Do not auto-select a template.

## Step 4. Read Inputs and Draft the Formal Article

Normalize the materials using [input-contract.md](input-contract.md).

Then:

- extract the source facts
- inspect template files if present
- keep a checklist of non-negotiable constraints
- write `metadata.json`
- write `article.html`
- place body images into `images/`

If the task mentions intermediate names like `output.local.html`, treat them as drafting intent and map the final managed output to `article.html`.

## Step 5. Prepare Images

- ensure article images live under `images/`
- if an image exceeds the upload limit, run `compress`
- do not alter non-content template images unless told to

## Step 6. Sync Every Completed Edit Round

- whenever a completed edit round changes `article.html` or article images, run `upload`
- after `upload` succeeds, immediately run `preview`
- if preview is generated and the environment supports it, show the QR code to the user or client
- do not end the round at local file edits only; sync and preview are part of completion
