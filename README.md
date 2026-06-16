# LA&LFD Obsidian Study Companion

This folder is an Obsidian-compatible companion to Gilbert Strang's *Linear Algebra and Learning from Data*. It is designed to sit beside handwritten notes: raw conversations are preserved as source material, while the durable ideas are distilled into structured topic notes.

## Structure

- `Home.md` is the top-level map of content.
- `Part I - ...` through `Part VII - ...` mirror the textbook.
- Each Part folder contains a `Part X MOC.md` note that lists notes and source conversations for that part.
- `Sources/` stores raw Gemini conversations and other unprocessed source material.
- `_templates/` stores reusable note templates.

## Workflow

1. Save a raw conversation in `Sources/` with a date prefix, for example `2026-06-16 Orthogonal Matrices and Eigenvalues.md`.
2. Add minimal frontmatter to the source note, but keep the transcript intact.
3. Create or update a polished topic note in the relevant Part folder.
4. Link the polished note back to the source note under `## Sources`.
5. Add the polished note to the relevant Part MOC.

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
- Use `part/1` through `part/7` for textbook parts.
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
- Keep `Home.md` and the Part MOCs updated as the vault grows.

## Math

Use Obsidian's built-in LaTeX rendering:

- Inline math: `$Q^TQ = I$`
- Display math:

```latex
$$
u(t) = c_1 e^{\lambda_1 t}x_1 + \cdots + c_n e^{\lambda_n t}x_n
$$
```
