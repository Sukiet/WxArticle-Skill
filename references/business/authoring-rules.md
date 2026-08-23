# Authoring Rules

## Writing Priorities

1. Keep facts correct.
2. Preserve mandatory template structure.
3. Respect explicit user constraints.
4. Improve clarity, selection, and rhetorical flow only inside the allowed range.

## What May Be Adapted

- article title and abstract, if the user did not lock them
- paragraph phrasing, while preserving factual meaning
- selection and ordering of highlights when the task is article recommendation
- short connective copy that helps the article read naturally

## What Must Not Be Changed Without Permission

- required template blocks and their nesting
- component spacing rules the user explicitly calls out
- canonical facts, quotations, numbers, and named entities from the source
- non-content template images or fixed remote assets
- upload, preview, and template selection decisions

## Local Versus Publish-Ready Image References

- During local drafting, use the article project's `images/` directory when the workflow expects local file references.
- If the user asks for a final publish-ready version, replace only the intended article image references with the required remote base URL plus file name.
- Keep template-owned remote image URLs untouched unless the user explicitly requests otherwise.

## Metadata Rules

`metadata.json` should reflect the formal article, not the template:

- `title`: final article title
- `abstract`: final article summary
- `article_uuid`: keep the initialized project id

Do not edit `created_at` or `modified_at` manually unless the toolchain explicitly requires it.

