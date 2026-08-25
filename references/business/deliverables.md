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

## Iteration Handoff Template

After each completed iteration, the user-facing reply should include all of the following:

- preview link
- preview QR code
- visual annotation link, or `后续将在 Lando 平台支持，当前版本暂未开放。`
- `article_uuid` in a code block when the user may approve the current version
- the exact closing sentence `如果您对注入流程不熟悉，也可以继续问我，我可以一步一步带您操作。`

Use this template:

````text
这次迭代已完成，您可以先查看这一版效果：

预览链接：
[preview_url]

预览二维码：
[renderable_qr]

可视化批注修改链接：
[annotation_url_or_unavailable_message]

如果您觉得这版没有问题，可以登录微信公众号后台进行推文注入。文章 UUID 我放在下面，方便您直接复制：

```text
[article_uuid]
```

如果您对注入流程不熟悉，也可以继续问我，我可以一步一步带您操作。
````

Do not automatically explain the injection steps, plugin installation, or backend workflow in this default handoff. Expand only when the user asks or appears blocked.
