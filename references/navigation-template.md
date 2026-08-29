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

## 1. Default entry（固定的人类入口页）

入口页是读者首先打开、直接给人看的成品。为避免每本书重新发明目录，固定使用以下顺序；不得把机器维护字段、审计信息或解析细节混入其中：

1. **书籍定位** — 一句话回答“这本书试图解决什么问题”。
2. **三项指标** — 精选卡片组数量、问题入口数量、原书页数。数量口径必须与 manifest 一致；精选卡片组默认包含全部已精选的 `S`/`A` 卡，并在说明中区分“最短路径（S）”与“补充理解（A）”。
3. **什么时候有用** — 用读者场景描述适用时机，而不是章节摘要。
4. **阅读提醒** — 只保留读者做判断所需的证据、地域、年代或安全边界；统计口径、PDF 解析规则、S/A 判定理由放入 `90_AI/<book-slug>/<book-title>｜蒸馏说明.md`。
5. **先看核心** — 先给一句推荐阅读链路；随后展示全部精选 `S`/`A` 卡，按 `reading_order` 升序。优先使用 Bases 卡片视图；同时提供折叠的静态 wikilink 列表作为无插件/预览模式的回退。卡片展示面只显示标题与 `display_summary`（约 30 字内），不展开 `problem`、长来源字段或审计元数据。
6. **章节地图** — 放在核心卡片与问题入口之间，按原书顺序提供四列：`章节｜PDF 页｜主要内容｜核心卡片`。章节地图是全书路线图，不重复卡片正文；PDF 只链接原文件页码。Markdown 表格内的 wikilink 别名分隔符必须写成 `\|`，否则会破坏列结构。
7. **按问题进入** — 展示全部已精选的问题入口，使用读者会提出的问句；每项链接到问题导航中的对应锚点。入口页在此结束，不再追加原文回读、继续探索、15/30/120 分钟路径或技术说明。

入口页可以有视觉样式，但信息职责不变：它只回答“我为什么看、先看什么、全书怎么走、我有什么问题”。原书文件仍可提供一个直达链接；全文转写只在来源模式例外时出现。

### 核心卡片视图实现（Obsidian）

若 vault 启用了 Bases，查询必须限定在当前书籍工作区的 `概念/`、`方法/`（以及经判定的 `案例/`）目录，筛选 `priority == "S"` 或 `priority == "A"`，按 `reading_order` 升序。卡片视图只显示 `file.name` 与 `display_summary`；不要把长问题、来源字段、证据等级或内部 ID作为入口卡片正文。查询结果应与静态回退列表逐项一致，而不是只显示前几张 S 卡。

可用的最小配置形状如下（字段名按宿主 Bases 版本调整，但语义不可改变）：

```yaml
filters:
  and:
    - or:
        - priority == "S"
        - priority == "A"
    - or:
        - file.folder == "20_Notes/Reading/<book-slug>/概念"
        - file.folder == "20_Notes/Reading/<book-slug>/方法"
properties:
  display_summary:
    displayName: 一句话说明
views:
  - type: cards
    order: [file.name, display_summary]
    sort:
      - property: reading_order
        direction: ASC
```

如果 Bases 不可用或渲染不稳定，保留一个按同一 `reading_order` 排列的折叠 wikilink 列表；不要为了视觉效果复制卡片文件或改写卡片内容。

## 2. Problem navigator

Phrase problems as questions a reader would actually ask, such as “我总是拖延，先改变什么？” or “怎样把理解变成输出？”. For an ordinary practical book, curate at least eight representative questions when the source supports them; if fewer are honest, state the smaller denominator.

Each problem row or block contains exactly:

1. **问题** — one concrete question, not a chapter label;
2. **首选卡** — one S/A card that should be opened first;
3. **配套卡** — zero to two cards for mechanism or implementation depth;
4. **原文锚点** — the most relevant original-source section/page. For a stable PDF, link directly to the original file with `#page=N` and a visible `PDF p. N` or range label;
5. **10分钟动作** — a start trigger, one observable behavior, an artifact or record, and a first success signal.

The navigator should give a three-click path from the entry page to the first-choice card. Do not list all related cards, duplicate card prose, or route the reader to a generic index before the first answer.

### 原文范围写法

每个重要问题至少提供一个带上下文的原文阅读单元，不要只写孤立的 `PDF p. N`。建议格式：

```md
原文回读：建议阅读 PDF p. 118–122（链接从 p. 118 打开）；核心命中页：p. 120
[[_attachments/Books/示例书.pdf#page=118|PDF p. 118–122（建议回读范围）]] · [[_attachments/Books/示例书.pdf#page=120|核心命中页 p. 120]]
```

普通命中点通常向前后扩展约 2–4 页，作为起点/通常上限而非凑页数规则；前后重复时可缩短。范围至少覆盖定义/前提、主张或步骤、关键例子/图表解释、限定/结论；图表还要含前定义与后解释，案例还要含情境→行动→结果→局限。遇到新小节、新案例、无关侧栏或论点转折立即切分；默认单元不超过 8 页，过长时拆分并说明目的。仅合并连续且同一逻辑单元的页面；相邻卡片窗口重复时优先合并窗口。链接只负责打开起始页，不转写范围内全文；无文本页、图表页或 OCR 不可靠时标注“请人工查看原 PDF”并设置 `manual_review: true`。

## 3. Structure/source index

This page is for completeness and machine retrieval, not the default reading experience. It contains:

- the chapter/section map in source order;
- each chapter's high-value themes and linked selected cards;
- explicit `已精选` and `暂不精选` labels, with a short reason for deferral such as repetition, background, or low transfer value;
- original source files, direct page/location anchors, evidence notes, any parsing limitations, and optional extraction units only when retained by exception;
- a complete list of stable card IDs and their source anchors.

The index may be detailed, but it should point to the entry and navigator instead of restating their reading advice. It is a structure/source lookup page, not a second default reading entry; its paths, selected/deferred labels, card IDs, and source anchors must agree with the final layout manifest.

## Link and duplication rules

- The default entry links to the navigator and index; the navigator links directly to cards and contextual source ranges; the index links to source units and all cards. Keep a separate core-page link only when it materially speeds verification.
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
