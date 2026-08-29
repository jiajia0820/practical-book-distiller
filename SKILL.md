---
name: practical-book-distiller
description: Use when an agent needs to turn an uneven-density practical book into a fast, problem-oriented reading package with selective deep links and source-traceable evidence; it is not for fiction, high-stakes legal or medical guidance, or research synthesis without routing first.
metadata:
  short-description: 按问题浏览实用书核心观点并回溯原文
---

# Practical Book Distiller

## 定位

This skill creates a **按需阅读导航器 + 可回溯证据层**. It helps a reader see the book's useful claims quickly, choose a relevant path, and return to the exact source when context matters. It is not a generic summary, sentence extractor, quote collector, or claim that a small card set covers the whole book.

The package is deliberately lossy but bounded: it compresses repetition and low-value narrative, records what was deferred, and keeps the original source as the canonical evidence. Never silently trade away a qualification that changes a claim's meaning.

## 适用与不适用

Use it for self-help, habits, productivity, management, communication, decision-making, and other practical books where information density is uneven and the reader wants to solve problems or test methods.

Before extracting, read [references/book-type-router.md](references/book-type-router.md). Route textbooks, research monographs, narrative works, and high-stakes legal/medical material to a safer workflow. A mixed book may be split by chapter type. If the source is incomplete, badly parsed, or lacks stable anchors, stop strong distillation and report the source limitation.

When the host is an Obsidian vault, also read [references/vault-layout.md](references/vault-layout.md) before creating or updating notes. The vault's `AGENTS.md`/`CLAUDE.md` and the user's explicit path choice take precedence. The layout contract is part of the deliverable: a logically good package is still defective if its files are scattered, duplicated, or hard to update.

## 工作原则

- Preserve the original source and make cards point back to it. For a stable PDF in a host that supports page deep links, use the original PDF page as the default evidence target; do not persist a full-text mirror merely for backtracing.
- Start from reader problems and high-value claims, not from a quota of cards or a demand to summarize every paragraph.
- Separate the author's assertion, the author's experience, anecdotes, reported studies, and independently checked evidence.
- Make methods executable: a reader should know how to start in ten minutes, what success looks like, and what single variable to adjust after failure.
- Prefer one primary card per problem and a short path to evidence; do not make every related note a front-door link.
- Treat quantity as adaptive. A dense 400-page book may deserve more cards than a repetitive 200-page book, but no book has a required card count.
- Do not create a persistent personal-understanding or practice-log feature unless the user explicitly asks for it.

## L0–L5 主流程

### L0 — 目标与类型路由

Identify the source, reader's current questions, desired depth, language, and output location. Classify the book and decide whether this skill is appropriate. Define a stopping rule before reading: stop adding cards when new material is repetitive, purely motivational, or cannot change a decision or action. Record high-stakes or missing-source exceptions rather than improvising. In an Obsidian vault, preflight the host rules and existing same-book notes, choose a stable book slug, and write a dry-run file manifest before creating notes. The manifest must distinguish `update`, `create`, `link-only`, `deferred`, and `conflict` items.

### L1 — 保全来源与建立证据层

Keep the original EPUB/PDF or an authorized source reference and choose a source mode before extraction. For a stable paginated PDF in an Obsidian vault, default to `pdf-direct`: cards and navigation pages link to `[[_attachments/Books/<book-file>.pdf#page=<N>|PDF p. <N>]]`. For a page range, link the first relevant page and display the full range; use separate links for separate passages. Text may be parsed temporarily to understand and verify the book, but do not persist a whole-book text/OCR mirror unless the user explicitly requests searchable full text or the host cannot reliably open the original source. Record parsing loss, OCR uncertainty, source mode, page/locator availability, and any retained fallback in the manifest. Do not repair uncertain text by guessing.

### 原文上下文窗口（PDF）

原文导航不能只留下孤立的命中页。对稳定 PDF，默认同时记录三个层次：

- **核心命中页**：最直接承载主张、步骤、图表或案例的页；
- **建议回读范围**：帮助读者理解前提、展开、例子和结论的连续页段；
- **链接起始页**：Obsidian 深链实际打开的范围首页，并在可见文字中显示完整范围。

普通概念或方法从命中页向前后扩展约 2–4 页；这是起点/通常上限，不是硬性凑页数规则：先按逻辑单元取范围，前后页重复时可以缩短。范围至少覆盖“定义/前提 → 主张或步骤 → 关键例子/图表解释 → 限定或结论”；遇到新小节、新案例、无关侧栏或论点转折就切分。单个阅读单元默认不超过 8 页，超出时命名并拆成多个单元。范围只是导航，不是全文转写。

图表范围应包含图表前的定义和图表后的解释；案例范围应包含情境、行动、结果与局限；只有连续且属于同一逻辑单元的页面才能合并。相邻卡片若目的相同且范围重叠，应合并阅读窗口，但保留各卡片自己的核心命中页。

图表、扫描页、无文本页或 OCR 不可靠的页面必须提示“请人工查看原 PDF”，并在来源记录中设置 `manual_review: true`；不得用推测性文字补齐。页码范围和起始页都必须在实际 PDF 页数内，并与 manifest 中的来源记录一致。

### L2 — 快速浏览与命题台账

Scan the table of contents, preface, conclusion, chapter openings, summaries, figures, and repeated terminology. Mark high-value themes, decision points, methods, and evidence-bearing passages. Build a claim ledger with: claim, problem served, priority, source anchor, evidence level, and whether it is selected or deferred. Aim for a small set of core propositions (usually 3–7), but let the book determine the final number.

### L3 — 选择性蒸馏

Read [references/card-schema.md](references/card-schema.md) before writing cards. Create only cards that materially improve retrieval or action:

- concept/principle cards for the author's reusable model or mechanism;
- method cards for a repeatable action or decision procedure;
- case/evidence cards only when a case has independent transfer value or is needed to prevent a core claim being misunderstood.

Read [references/evidence-policy.md](references/evidence-policy.md) whenever a card contains evidence, research, numbers, or quotations. Every selected S-level proposition must have an accurate chapter/section anchor. If context is needed to interpret it, include the necessary qualification in the card and link to the original source location. For PDF anchors, provide a recommended context range and, when useful, a separate core hit-page link; the link opens the range's first page. Retain an extracted-text fallback only under the explicit conditions in L1.

### L4 — 入口与按问题导航

Read [references/navigation-template.md](references/navigation-template.md). Produce three distinct roles: one default entry, one problem navigator, and one structure/source index. For each meaningful problem provide one first-choice card, no more than two supporting cards, an original-source anchor, and a ten-minute starting action. The full book map must distinguish selected topics from intentionally deferred topics so the reader cannot mistake the package for total coverage. Place these pages and book-scoped cards under the canonical `20_Notes/Reading/<book-slug>/` workspace from [references/vault-layout.md](references/vault-layout.md); do not flatten a book's files into the Reading root. The global reading index should link only to the entry page.

### L5 — 结构与语义验收

Run both checks below and report evidence. Structural checks prove the package is intact; semantic checks prove that a reader can use it. Fix errors before handoff or disclose the exact residual risk.

## 输出契约

The deliverable contains, as applicable:

1. **Source artifact** — the original file or a stable source link, retained according to workspace and copyright rules.
2. **Source backtrace** — direct links to the original file at reliable pages/locations. A retained searchable text layer is optional, not the default, and must state why direct source access is insufficient or that the user requested it.
3. **Selective cards** — concept/principle and method cards with stable IDs, restrained fields, priorities, evidence labels, and source backtraces. Independent case cards are exceptional.
4. **Reading navigation** — a default entry, problem navigator, and structure/source index with non-overlapping responsibilities.
5. **Scope note** — core propositions, selected topics, deferred topics, source limits, and any claims deliberately excluded.
6. **Layout manifest** — the book slug, canonical paths for every logical role, source/work-product paths, `create` versus `update` decisions, unresolved conflicts, and the rerun strategy. A dry-run manifest is produced before writing; the final machine-readable manifest is canonically stored at `90_AI/<book-slug>/manifest.yaml` (or one declared JSON equivalent) and updated after writing.

Follow host workspace rules for folders, wikilinks, naming, and attachments. Do not copy the complete book into this skill directory and do not overwrite unrelated notes. Keep book-scoped cards in `20_Notes/Reading/<book-slug>/概念/`, `方法/`, or (only when justified) `案例/`. Promote a card to `30_Knowledge/` only when it is explicitly judged reusable across books and the canonical relationship is recorded. On rerun, update/merge existing canonical files by stable ID; never create a duplicate flat file or silently move/rename an old note.

## 最小字段契约

All cards use the common metadata in [references/card-schema.md](references/card-schema.md): stable `id`, `kind`, `priority`, `problem`, `source_chapter`, `source_location`, `anchor_granularity`, and (when relevant) `evidence_level`. Omit optional fields that have no content; never fill a field with generic prose merely to satisfy a template.

Concept cards must state a conclusion, the problem it solves, the mechanism, source-grounded explanation, examples/evidence with attribution, credibility boundary, application, and an original-source link.

Method cards must state the goal, principle, minimum steps, a ten-minute start, when to use it, failure and one-variable adjustment rules, a success threshold/verification metric, and the original-source link.

## 证据边界与回退

Use the labels and anchor rules in [references/evidence-policy.md](references/evidence-policy.md). A book's report of a study is still a second-hand report until the primary source is inspected; never upgrade it to verified evidence. Never invent citations, sample sizes, quotations, page numbers, or causal strength. When parsing loses a qualifier or the anchor is uncertain, downgrade or omit the claim and point the reader to the source for manual checking.

## 失败防线

- **伪全书覆盖**: publish selected/deferred status and a chapter map; card count is never a coverage metric.
- **摘要堆积**: delete duplicated explanations and stories unless they change interpretation, transfer, or action.
- **证据幻觉**: attach an evidence label and precise anchor; use “作者声称/书中转述” rather than implying validation.
- **错误回溯**: check the card against the actual section, not the chapter title guessed from memory; do not reduce a contextual passage to a single page when the logic spans several pages.
- **导航重复**: one default entry, one problem navigator, one source index; cross-link rather than repeat lists.
- **不可执行的方法**: no method card without a ten-minute start, success threshold, and adjustment rule.
- **模板主义**: fields are a minimum contract, not a reason to create a card for every chapter or leave empty sections.
- **高风险越界**: route legal, medical, and scientific claims to the book-type router; do not turn them into personalized advice.

## 验收标准

### 结构验收

- At least one original source or stable source reference is preserved. PDF anchors open the original file at valid pages when the host supports deep links. Each important anchor has a visible recommended context range plus a core hit page where applicable; the range starts at the linked page. A retained text/evidence mirror exists only when explicitly requested or needed as a documented fallback.
- All wikilinks/links resolve; there are zero duplicate knowledge IDs; every card has a stable ID and source backtrace.
- For PDF cards with contextual anchors, `source_context_start <= source_core_page <= source_context_end`; all three pages are within the PDF when a core page is declared.
- The three navigation roles are present and do not duplicate each other.
- The package has zero unresolved scaffold markers and states all intentional omissions.
- The final manifest names one canonical `20_Notes/Reading/<book-slug>/` workspace. The Reading root contains no new flat entry, navigator, index, concept card, or method card for this book.
- Concept and method cards are physically grouped under the book workspace's `概念/` and `方法/` directories; exceptional case/full-text directories are created only when justified. Any `30_Knowledge/` card has an explicit cross-book reuse decision and a link back to its book-scoped source.
- Original binaries and derived work products obey the host paths (normally `_attachments/Books/` and `90_AI/<book-slug>/`). The global reading index links to the book entry only.
- A rerun against the same source reuses the recorded slug, deterministic card IDs, and canonical paths, and produces no duplicate “副本/新版/2” files. If the manifest is missing or ambiguous, matching falls back to canonical paths plus ISBN/source hash/stable IDs and stops on unresolved conflicts. Existing notes are not moved or renamed without explicit authorization.

### 语义验收

- Curate at least eight representative problem prompts for an ordinary practical book. If the book genuinely supports fewer, state the smaller denominator; never invent problems to meet a quota.
- In a usability test, at least 90% of those prompts reach the first-choice card within three clicks.
- A reader can move from a chosen problem to a core conclusion and one action within fifteen minutes.
- 100% of S-level propositions have accurate chapter/section anchors and an evidence label.
- For every S-level or otherwise important PDF anchor, verify the context fields and reason; chart/case/method/argument-turn windows are not single-page unless the source itself is genuinely one page and the exception is stated.
- Every method card can be started within ten minutes and defines a success threshold plus a one-variable adjustment rule.
- Manually sample high-value topics from the table of contents and assess proposition coverage; do not infer quality from card count.
- Report unresolved parsing loss, weak evidence, or unverified anchors instead of claiming certainty.
- For sampled high-value anchors, confirm that the recommended context range contains the necessary setup and qualification, not just the keyword hit page; confirm range endpoints are within the PDF page count.

At handoff, list files, line counts, validation commands and outputs, and the remaining human-review judgments (especially source accuracy, priority, and whether a method transfers beyond the book's examples).
