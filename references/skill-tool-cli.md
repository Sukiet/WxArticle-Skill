# Skill Tool CLI

This skill package does not ship with `skill-tool.exe` by default. Install it only after the user approves. Use [install.md](install.md) when the tool is missing and [update-check.md](update-check.md) when checking whether the installed version should be updated.

## Bundled Runtime Layout

The packaged skill expects these files:

```text
assets/
  skill-tool/
    skill-tool.exe
    .env
```

`skill-tool.exe` looks for `.env` in this order:

1. current working directory
2. executable directory
3. parent directory of the executable directory

Because of that, change the working directory to `assets/skill-tool/` before invoking `skill-tool.exe`.

## Config Variables

- `WX_ARTICLE_REPO_DIR`
  The root directory that will contain article projects.
- `WX_ARTICLE_HOST`
  The backend host used by the CLI.

Rule:

- `WX_ARTICLE_REPO_DIR` may be updated after user confirmation so the article workspace lives outside the skill package.
- Sensitive future config such as access tokens should not be rotated or replaced casually during ordinary drafting work.

## Commands

### `init`

Create a new managed article project under `WX_ARTICLE_REPO_DIR`.

Outputs include:

- `article_uuid`
- project directory
- `metadata.json`
- `article.html`

### `work-dir -a {article_uuid}`

Resolve the local project paths for an existing article id.

Use this when:

- you already know the `article_uuid`
- you need to reopen or inspect that article's local workspace
- you want the canonical paths before reading or updating project files

Typical returned paths include:

- `project_dir`
- `metadata_path`
- `article_html_path`
- `images_dir`
- `metadata.example.json` path
- `example.html` path

### `templates-list`

List available backend templates. Use this only when the user wants to choose a template.

### `fetch-template -a {article_uuid} -t {template_uuid}`

Pull template files into the existing article project.

Creates:

- `metadata.example.json`
- `example.html`

### `compress -a {article_uuid} -n {image_name}`

Compress one oversized image in `images/` in place. Use only when the image exceeds the upload limit or upload tells you to compress first.

### `upload -a {article_uuid}`

Upload the formal article metadata, HTML, and images.

For this skill's workflow:

- run `upload` after every completed modification round that changes `article.html` or files in `images/`
- do not stop at local file updates if the edit round is considered finished

### `preview -a {article_uuid}`

Generate preview info and a QR code path.

For this skill's workflow:

- run `preview` immediately after each successful `upload`
- surface the QR code to the user or client right away

## Output Convention

All commands return JSON. Key fields commonly include:

- `ok`
- `message`
- `next_commands`
- `suggested_prompt`
- `error`

Treat `next_commands` as optional suggestions, not mandatory instructions.
