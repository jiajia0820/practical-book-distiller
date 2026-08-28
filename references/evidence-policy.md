# Evidence Policy

This policy prevents an elegant card from making a source sound more certain than it is. Evidence labels describe what the book actually supplies; they are not a quality score and do not replace independent verification.

## Original-file-first anchors

The original source is the canonical evidence. Do not create or retain a whole-book Markdown/OCR mirror merely so cards have something to link to.

For a stable PDF in an Obsidian vault, use a direct page link:

```markdown
[[_attachments/Books/<book-file>.pdf#page=<N>|PDF p. <N>]]
```

- For `PDF p. 123–127`, use `#page=123` as the target and keep the visible range in the alias.
- For separate passages, create separate page links rather than one vague chapter link.
- Validate that every `N` is within the source PDF page count and sample-open high-priority anchors.
- If the host cannot deep-link, link the original file and display the exact page/chapter/locator next to it. Do not replace the missing deep link with an unnecessary text mirror.

`#page=N` means the PDF viewer's 1-based page index, not necessarily the printed page label shown inside the book. Record a separate `printed_page_label` when the distinction matters; never silently add a front-matter offset.

Text extraction may be used temporarily during distillation. Persist a searchable evidence layer only when the user explicitly requests it or the original file cannot be reliably opened/located in the host; record that exception in the manifest.

## Evidence levels

Use one of these labels whenever a card contains a claim that sounds factual, causal, numerical, or research-based:

| Label | What it means | Safe wording |
|---|---|---|
| `author_claim` | The author states an interpretation, principle, or recommendation | “作者主张/本书提出……” |
| `author_experience` | The author reports their own experience, observation, or practice | “作者自述……” |
| `anecdote` | A person or case is narrated as an illustration | “书中举例说明……”；不要写成普遍证明 |
| `reported_research` | The book paraphrases or cites a study that was not inspected in the original | “书中转述一项研究……”；不得称为已核验证据 |
| `primary_research` | The original paper, dataset, experiment, law, or official record was inspected and its relevant context is available | “原始来源显示……”；仍需保留限制条件 |
| `analogy` | A metaphor or comparison used to explain an idea | “作者用……类比……”；不是证据 |

When several levels appear, label each passage or use the lowest level supporting the conclusion. A reported study never becomes `primary_research` merely because the book supplies a citation or a confident number.

## Attribution and claim strength

- Attribute the claim to the author unless an independently inspected source supports it.
- Preserve whether the source says “may”, “often”, “associated with”, or “causes”. Do not strengthen modality during paraphrase.
- Do not turn an author's metaphor about the brain, psychology, or society into a scientific mechanism.
- Do not invent a study name, author, sample size, percentage, quotation, page, or causal explanation. If the source is vague, keep the wording vague and point back to it.
- Separate facts supplied by the source from the distiller's interpretation. Mark any synthesis as an interpretation and link all contributing anchors.

## Source fields and anchor granularity

Every selected card has:

- `source_chapter`: the actual chapter/part title or number in the retained source;
- `source_location`: the actual heading, page, paragraph range, EPUB location, or other stable locator;
- `anchor_granularity`: the narrowest reliable level: `section`, `subsection`, `page`, `paragraph`, or `chapter`.

Prefer `subsection` or `paragraph` when the source exposes headings or stable offsets. Use `page` only when pagination is reliable for the source edition. Use `chapter` as a last resort and state that surrounding context must be read. Never infer a location from a card title or a remembered table of contents.

The source anchor should open the original file at the relevant point whenever the source and host support it. If the host cannot deep-link, include the original-file link and a human-readable locator; add an extracted unit only when the retained-fallback condition above is met. A broken or ambiguous anchor is a quality defect, not a cosmetic issue.

## Parsing loss and fallback

Record extraction/OCR loss when it affects punctuation, negation, numbers, references, tables, figures, or section order. If a lost token could change interpretation:

1. Do not state the claim as settled.
2. Downgrade its priority or evidence level, or omit the card.
3. Link to the original source and identify the exact passage that needs human checking.

If an entire chapter or source segment is unavailable, keep a source-audit note and mark the affected topics as unverified/deferred. Never fill gaps with a likely quotation or outside memory. A retained evidence layer is an exceptional fallback for access or an explicit user request, not a default deliverable and not permission to copy the whole book into a card.

## Review gates

Before handoff, manually inspect every S-level card and every card containing research, numbers, causal language, or a quote. Confirm that the evidence label, source chapter, source location, and claim strength all match the source. The agent may report “source says X; independent verification not performed” and still deliver a useful navigator; it must not hide that limitation.

