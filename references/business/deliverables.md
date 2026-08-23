# Deliverables

## Canonical Project Outputs

The managed article project should end in this shape:

```text
{WX_ARTICLE_REPO_DIR}/{article_uuid}/
  article.html
  metadata.json
  images/
```

If a template was fetched, the same directory may also contain:

```text
metadata.example.json
example.html
```

## What to Hand Back to the User

At minimum, summarize:

- the workspace directory
- the project directory
- the `article_uuid`
- whether the article uses a template
- whether `article.html`, `metadata.json`, and `images/` are ready

## Intermediate Naming

If the user's source prompt mentions names like `output.local.html` or `output.html`, treat those as intent-level names, not the managed storage contract. The canonical file inside the project remains `article.html`.

## Upload and Preview State

Each finished modification round should end in the last two states below, not just a local draft:

- draft completed locally, not uploaded
- uploaded successfully
- preview prepared
- upload blocked because files or images still need attention

Preferred completion pattern:

- `article.html` or `images/` changed
- `upload` completed successfully
- `preview` completed successfully
- QR code shown to the user or client

