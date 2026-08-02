# LA&LFD Obsidian Study Companion

This folder is an Obsidian-compatible companion to Gilbert Strang's *Linear Algebra and Learning from Data*. It is designed to sit beside handwritten notes: raw conversations are preserved as source material, while the durable ideas are distilled into structured topic notes.

Scope is **Part I - Highlights of Linear Algebra**. The other six parts of the book are deliberately out of scope and are not represented here.

## Structure

- `Home.md` is the single map of content: the Part I section list, the polished notes, and the source conversations.
- `I.1 - ...` through `I.12 - ...` are one folder per Part I section, mirroring the textbook.
- Each section folder holds its polished topic note alongside the raw conversations that fed it.
- `_templates/` stores reusable note templates.

Empty section folders carry a `.gitkeep` so the scaffolding survives a clone. Delete it once the folder has a real note.

## Workflow

1. Save a raw conversation in the relevant section folder with a date prefix, for example `I.6 - Eigenvalues and Eigenvectors/2026-06-16 Orthogonal Matrices and Eigenvalues.md`.
2. Add minimal frontmatter to the source note, but keep the transcript intact.
3. Create or update the polished topic note in the same section folder.
4. Link the polished note back to the source note under `## Sources`.
5. Add the polished note to `Home.md`.

## Naming

Use textbook section numbers for polished notes:

```text
I.6 - Eigenvalues of Orthogonal and Symmetric Matrices.md
```

Use date-prefixed descriptive names for raw conversations:

```text
2026-06-16 Orthogonal Matrices and Eigenvalues.md
```

## Frontmatter

Polished notes should use this shape:

```yaml
---
title: Eigenvalues of Orthogonal and Symmetric Matrices
book: Linear Algebra and Learning from Data
part: I
section: I.6 Eigenvalues and Eigenvectors
pages:
status: seedling
created: 2026-06-16
tags: [type/topic, status/seedling, part/1, section/I-6, eigenvalues]
related: []
sources: ["[[2026-06-16 Orthogonal Matrices and Eigenvalues]]"]
---
```

Raw source notes should use this shape:

```yaml
---
title: Orthogonal Matrices and Eigenvalues
type: source
source: Gemini
created: 2026-06-16
tags: [type/source, part/1, section/I-6, eigenvalues]
---
```

## Tags

- Use `type/topic`, `type/source`, and `type/moc` to distinguish note types.
- Use `part/1` on every note, since Part I is the whole scope.
- Use `section/I-6` style tags for textbook sections.
- Use topic tags such as `eigenvalues`, `orthogonal-matrices`, `symmetric-matrices`, `normal-matrices`, `differential-equations`, and `complex-eigenvalues`.
- Use `status/seedling`, `status/budding`, and `status/evergreen` to track maturity.

## Status

- `seedling`: first good version, useful but still open to refinement.
- `budding`: revised after more textbook work or problem solving.
- `evergreen`: stable reference note worth relying on during review.

## Linking

- Prefer Obsidian wikilinks: `[[I.6 - Eigenvalues of Orthogonal and Symmetric Matrices]]`.
- Put related concepts under `## Connections`.
- Put raw conversations under `## Sources`.
- Keep `Home.md` updated as the vault grows.
- Wikilinks resolve by filename, so notes can be moved between section folders without breaking links.

## Math

Use Obsidian's built-in LaTeX rendering:

- Inline math: `$Q^TQ = I$`
- Display math:

```latex
$$
u(t) = c_1 e^{\lambda_1 t}x_1 + \cdots + c_n e^{\lambda_n t}x_n
$$
```
