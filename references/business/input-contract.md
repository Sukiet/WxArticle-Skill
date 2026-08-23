# Input Contract

Normalize the user's delivery into three buckets before drafting:

## 1. Content Information

Treat these as the factual source materials that the article must be based on.

Common forms:

- source documents such as `.docx`, `.pdf`, `.md`, or plain text notes
- source images that belong to the article body
- article abstracts, summaries, bullet notes, or pasted research excerpts
- directory-based source packages where a document defines the canonical text

Rules:

- Prefer the explicitly named canonical source when the user says one file is authoritative.
- Extract facts faithfully before rewriting for style.
- When the article is for recommendation or promotion, select the highlights, but do not invent facts beyond the source.

## 2. Template Information

Treat these as style and structure references rather than final content.

Common forms:

- `example.html`
- `metadata.example.json`
- a fetched backend template
- a previously published article that acts as layout reference

Rules:

- Distinguish template content from target content.
- Reuse layout, block order, tone, and field patterns as instructed.
- If the user says the template is mandatory, preserve its component structure and outer boundaries.

## 3. Restrictive Instructions

Treat these as the highest-priority production rules.

Typical examples inferred from the user's prompt package:

- which file is the canonical content source
- whether the template structure may or may not change
- whether certain components, spacing, or wrappers must stay untouched
- whether the article should emphasize selected highlights rather than the full source
- whether article images must be extracted to `images/`
- whether local file references must later be converted into remote publish URLs

Rules:

- If a restrictive instruction conflicts with stylistic preference, follow the restrictive instruction.
- If multiple constraints conflict with each other, stop and surface the conflict clearly.
- Keep a short working checklist of the non-negotiable constraints while drafting.

