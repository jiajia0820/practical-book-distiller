# Card Schema

Cards are retrieval units, not miniature chapters. Use the smallest card that lets a reader understand the claim or begin the method, then link to the original source at the narrowest reliable location. A retained text layer is an explicit exception, not the default. The number of cards is determined by distinct problems and transferable claims; it is never fixed by book length or by this schema.

## Common metadata

Every selected card has these machine-readable fields:

| Field | Allowed form | Rule |
|---|---|---|
| `id` | Stable book-scoped slug | Never reuse an ID for a different claim; keep it stable when prose is edited |
| `kind` | `concept`, `method`, or exceptional `case` | A case is not the default container for every story |
| `priority` | `S`, `A`, or `B` | `S` = first-read core, `A` = useful support, `B` = optional context |
| `problem` | One or more problem labels | Use reader language; do not hide a card behind only chapter names |
| `source_chapter` | Actual chapter/part title or number | Required for every card |
| `source_location` | Actual section heading, page, paragraph range, or stable locator | Use the narrowest locator the source supports; never invent a page |
| `anchor_granularity` | `section`, `subsection`, `page`, `paragraph`, or `chapter` | Coarse granularity requires a context warning and an original-source fallback; use retained text only when the source-mode exception permits it |
| `evidence_level` | Value from evidence policy | Required when a card makes an evidence, research, numerical, or causal claim |

For a paginated PDF, cards that depend on surrounding context should also expose (in frontmatter or a clearly labelled body block) `source_context_start`, `source_context_end`, `source_core_page`, and a short `context_reason`; set `manual_review: true` for chart/image/OCR pages. The range's deep link opens its first page; it is a navigation window, not a copied text block. Keep endpoints within the actual PDF. S-level claims with a distinct page hit must provide `source_core_page`; omit it only for a pure chapter/section anchor with no single useful hit page.

Use normal Obsidian frontmatter or the host system's equivalent. Keep IDs ASCII and human-auditable. Preserve wikilinks and source URLs where the host supports them. Omit optional fields rather than filling them with boilerplate.

For cards surfaced on the human entry page, add two display fields:

```yaml
reading_order: 1                 # positive integer; required for selected S/A cards
display_summary: 一句话说明卡片用途   # reader-facing, normally ≤30 Chinese characters
```

`reading_order` is book-scoped and deterministic; do not use file creation time or chapter number as a substitute. Assign contiguous order to the selected S/A set when practical, and preserve existing values on rerun unless the user intentionally changes the reading path. `display_summary` explains why a reader might open the card; it is not a second conclusion, evidence paragraph, or safety disclaimer. Cards without these fields may remain in the source index/problem navigator but must not silently appear in the entry's core-card view.

## Concept/principle card

Create this card only when the book offers a reusable model, distinction, mechanism, or decision principle. The body contains:

1. **结论** — the author's claim in plain language, with attribution where needed.
2. **它在解决什么问题** — the reader situation this claim helps interpret or decide.
3. **核心机制** — the causal or conceptual chain, without upgrading a metaphor into science.
4. **书中解释** — a compact, context-preserving paraphrase tied to the source.
5. **依据与例子** — clearly labelled author experience, anecdote, reported study, or checked evidence.
6. **可信度边界** — what the source does not establish, what is contested, and when to read the original context.
7. **如何应用** — one or two concrete uses, not a generic motivational slogan.
8. **原文回溯** — a working link or locator using the common metadata, with a context range and optional core hit page for PDF sources.

If a concept has no distinct mechanism or application, keep it in the claim ledger or chapter map instead of making a card.

## Method card

Create this card when a reader can repeat an action, routine, checklist, or decision procedure. The body contains:

1. **目标** — the observable problem or outcome.
2. **原理** — why the author expects the method to help, labelled as a source claim.
3. **最小步骤** — the shortest ordered procedure that preserves the method's logic.
4. **10分钟启动动作** — a concrete first attempt that produces an artifact or observable behavior.
5. **何时使用** — the trigger or situation in which the method is relevant.
6. **失败与调整** — common failure signal and exactly one variable to adjust before retrying.
7. **成功阈值/验证指标** — a time window, count, quality bar, or other observable threshold; avoid vague “坚持下去”.
8. **原文回溯** — a working link or locator using the common metadata, with a context range and optional core hit page for PDF sources.

A method without a start action, success threshold, or adjustment rule is an idea, not an executable method card.

## Exceptional case/evidence card

Do not create an independent case card merely because the book contains a story. Create one only when the case is independently transferable, supplies essential context for an S-level claim, or is the only way to distinguish a reported finding from an author's assertion. Keep it compact:

- **情境** — who/what/when, without adding facts not in the source;
- **它支持的主张** — the exact claim it illustrates;
- **证据类型** — one evidence label from the evidence policy;
- **可迁移启示** — what a reader may cautiously reuse;
- **局限** — why the case does not prove a general causal rule;
- **原文回溯** — exact source anchor.

If the case can fit in a concept or method card without losing meaning, embed it there and do not create a separate note.

## Priority and selection rules

- Mark a card `S` only if omitting it would materially weaken the book's core argument or the reader's first action path.
- Mark `A` for useful mechanisms or methods that support an S card or solve a common secondary problem.
- Mark `B` for optional context, a non-essential example, or a useful but weakly supported extension.
- A low priority does not mean false; it means “not a first stop”.
- Maintain a selected/deferred ledger at book level so readers can see what was intentionally left in the original source. If a retained text layer exists by exception, name it explicitly in the manifest.
