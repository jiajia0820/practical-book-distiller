# Navigation Template

The package has three page roles. Keep their jobs distinct so the reader always knows whether they are choosing a path, solving a problem, or checking the source structure.

## Physical location

In an Obsidian vault, all three pages live in one book workspace:

```text
20_Notes/Reading/<book-slug>/
├─ <book-title>｜入口.md
├─ <book-title>｜问题导航.md
└─ <book-title>｜结构与来源索引.md
```

The entry may link to cards in `概念/`, `方法/`, and an exceptional `案例/` directory. Use canonical, vault-resolvable wikilinks and preserve the slug from the layout manifest. Do not create another entry, navigator, or index under `20_Notes/Reading/` root, and do not duplicate a card merely to make a link convenient. The global `读书笔记索引.md` links to this book's entry only.

## 1. Default entry

The default entry is the first page a reader opens. Keep it short enough to scan in one screen where practical. It contains:

- the book title, author, source status, and one attributed sentence describing the book's central promise;
- a “when this is useful” note and the main caveat about evidence or scope;
- the S-level core propositions in reading order, each linked to its card;
- a 15-minute path: choose one problem, read its first-choice card, open the source anchor only if needed, and perform one ten-minute action;
- links to the problem navigator, structure/source index, and original source file; include a retained text layer only when the source-mode exception requires it.

The entry page is a launchpad. It must not reproduce every card, chapter, metadata field, or evidence note.

## 2. Problem navigator

Phrase problems as questions a reader would actually ask, such as “我总是拖延，先改变什么？” or “怎样把理解变成输出？”. For an ordinary practical book, curate at least eight representative questions when the source supports them; if fewer are honest, state the smaller denominator.

Each problem row or block contains exactly:

1. **问题** — one concrete question, not a chapter label;
2. **首选卡** — one S/A card that should be opened first;
3. **配套卡** — zero to two cards for mechanism or implementation depth;
4. **原文锚点** — the most relevant original-source section/page. For a stable PDF, link directly to the original file with `#page=N` and a visible `PDF p. N` or range label;
5. **10分钟动作** — a start trigger, one observable behavior, an artifact or record, and a first success signal.

The navigator should give a three-click path from the entry page to the first-choice card. Do not list all related cards, duplicate card prose, or route the reader to a generic index before the first answer.

## 3. Structure/source index

This page is for completeness and machine retrieval, not the default reading experience. It contains:

- the chapter/section map in source order;
- each chapter's high-value themes and linked selected cards;
- explicit `已精选` and `暂不精选` labels, with a short reason for deferral such as repetition, background, or low transfer value;
- original source files, direct page/location anchors, evidence notes, any parsing limitations, and optional extraction units only when retained by exception;
- a complete list of stable card IDs and their source anchors.

The index may be detailed, but it should point to the entry and navigator instead of restating their reading advice. It is a structure/source lookup page, not a second default reading entry; its paths, selected/deferred labels, card IDs, and source anchors must agree with the final layout manifest.

## 15/30/120-minute paths

Offer time-based paths only when they reduce choice cost:

- **15 minutes**: one problem, one first-choice card, one ten-minute action, and one source check if a caveat matters;
- **30 minutes**: the same problem plus up to two support cards and the relevant chapter context;
- **120 minutes**: the S-level map, several problem paths, and selected original-source passages; still do not imply that the whole book has been read.

These paths are shortcuts into the same original source, not separate summaries or text mirrors that can drift apart.

## Link and duplication rules

- The default entry links to the navigator and index; the navigator links directly to cards and anchors; the index links to source units and all cards.
- A card owns its explanation. Navigation pages own ordering and choice, not repeated prose.
- Keep one canonical title and ID per concept or method. If two chapter discussions are merged, list both source anchors in the card.
- Avoid a separate case page unless the card schema's transfer-value test is met; embed ordinary examples in the parent card.
- If a problem has no trustworthy card or source anchor, mark it as “需回原文/未覆盖” instead of linking a vaguely related note.
- Card filenames should not repeat the full book title when they already sit inside the book workspace. If a cross-book card is promoted to `30_Knowledge/`, retain a canonical link to the book-scoped card rather than creating two independently editable explanations.

## Usability test

Before handoff, test at least eight problem prompts (or all honest prompts for a smaller book):

1. Start at the default entry.
2. Count clicks until the first-choice card is visible.
3. Check that the card answers the question without requiring a full-text detour.
4. Verify that the source anchor reaches the relevant passage.
5. Confirm that the ten-minute action has a trigger, behavior, artifact, and success signal.

Target a first-choice hit within three clicks for at least 90% of prompts and a problem-to-conclusion-plus-action path within fifteen minutes. Record misses and fix the navigation role or card priority; do not solve misses by adding more links to every page.

