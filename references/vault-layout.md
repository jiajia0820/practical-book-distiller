# Vault layout contract

本参考文件定义把蒸馏包写入 Obsidian vault 时的物理目录契约。逻辑角色（入口、问题导航、结构/来源索引、卡片、证据层）只有映射到稳定路径后，才能被人和 AI 长期检索。宿主 vault 的 `AGENTS.md`、`CLAUDE.md` 或用户明确指定的位置优先于本文件。

## 预检与范围

1. 在创建或更新文件前，读取当前 vault 根目录及相关父目录的 `AGENTS.md`/`CLAUDE.md`，并记录其中关于命名、链接、附件和已有笔记的规则。
2. 检查 `20_Notes/Reading/`、`90_AI/`、`_attachments/Books/`、`30_Knowledge/` 和全局读书索引中是否已经有同一书名、ISBN、源文件哈希或稳定卡片 ID。找到已有包时进入 update/merge 模式，不另起一套平铺副本。
3. 先生成一份 dry-run manifest，再写文件。最终 manifest 的 canonical path 固定为 `90_AI/<book-slug>/manifest.yaml`（若宿主明确要求 JSON，可使用同目录的 `manifest.json`，但同一本书只能有一个 canonical manifest）。manifest 至少列出书籍 slug、每个逻辑角色的 canonical path、将更新的已有文件、将新建的文件、来源文件和未决冲突，并为每个文件标记 `update`、`create`、`link-only`、`deferred` 或 `conflict`。
4. 本流程不自动移动、不自动重命名或删除旧笔记；旧笔记可能已有 wikilink。只有用户明确要求迁移时，才另行提出迁移计划并逐条修复链接。

最小机器可读结构如下；字段可扩展，但不得省略书籍身份、版本、路径、状态和冲突：

```yaml
schema_version: 1
book_slug: example-book
source:
  mode: pdf-direct
  paths: [_attachments/Books/example-book.pdf]
  page_count: 270
  page_numbering: pdf-viewer-1-based
  isbn: null
canonical:
  entry: 20_Notes/Reading/example-book/example-book｜入口.md
  navigator: 20_Notes/Reading/example-book/example-book｜问题导航.md
  index: 20_Notes/Reading/example-book/example-book｜结构与来源索引.md
  ai_note: 90_AI/example-book/example-book｜蒸馏说明.md
  evidence: null
files:
  - path: 20_Notes/Reading/example-book/概念/核心模型.md
    role: concept-card
    status: create
    id: example-book-concept-core-model
conflicts: []
rerun:
  match_keys: [stable_id, canonical_path, isbn, source_hash]
  on_ambiguous_match: stop_and_report
```

## 默认物理拓扑

每本书拥有一个独立工作区，禁止把该书的入口、问题导航或 book-scoped 卡片平铺到 `20_Notes/Reading/` 根目录：

```text
20_Notes/Reading/<book-slug>/
├─ <book-title>｜入口.md
├─ <book-title>｜问题导航.md
├─ <book-title>｜结构与来源索引.md
├─ 概念/
│  └─ <concept-name>.md
├─ 方法/
│  └─ <method-name>.md
├─ 案例/                 # 只有案例通过迁移价值检查时创建
│  └─ <case-name>.md
└─ 全文/                 # 仅用户明确要求持久化全文时创建
   └─ <chapter-or-section>.md
```

- `<book-slug>` 是稳定、短且文件系统安全的目录名；优先使用已有目录名，否则由书名生成并在 manifest 固定。不要因再次运行而变更 slug。
- 入口、问题导航和结构/来源索引各只有一份。入口文件名可以保留完整书名；卡片文件名不重复整本书名，因为父目录已经提供书籍上下文。
- `概念/` 放只服务本书的 principle/concept 卡，`方法/` 放只服务本书的 method 卡，`案例/` 仅放具有独立迁移价值的案例卡，`全文/` 仅在用户明确要求持久化全文时生成。普通例子嵌回所属卡片，不为每个故事建文件。
- 读书包默认只在本书工作区内互链。跨书且稳定、可复用、用户明确需要长期沉淀的知识，才复制/提炼为 `30_Knowledge/<concept-name>.md`，并在原卡片注明 canonical card 和来源；不要把所有 book-scoped 卡片自动升级为全局知识卡。

## 来源与工作产物

- 原始 PDF/EPUB、封面和二进制附件放在 `_attachments/Books/`（若宿主已有更具体的书籍附件目录，遵循宿主规则并在 manifest 记录）。不要把原书复制进 skill 目录。
- `90_AI/<book-slug>/` 默认保留 manifest、统一的 `<book-title>｜蒸馏说明.md`（机器维护的统计口径、S/A 选择理由、PDF 解析规则、证据边界、重跑规则和 Bases 实现规则）以及解析损失和确有必要的转换记录。文本/OCR 可在蒸馏过程中临时使用，但不持久化整本镜像；只有用户明确要求全文检索，或原文件无法可靠打开/定位时，才保留证据层并在 manifest 写明原因。
- 人类入口只保留读者作判断所需的最小提醒；不要把上述 AI 说明复制到入口。入口、问题导航和结构/来源索引可以互相链接，但每种角色只维护一份 canonical 内容。
- `20_Notes/Reading/读书笔记索引.md`（如存在）只链接每本书的入口页，不逐张列出卡片；新书只增加一个入口链接。

## 命名、链接与 ID

- 人类可见文件使用清晰中文名；slug 去除路径分隔符、控制字符和不稳定的版本/日期后缀，保留足以辨识书籍的名称。
- 每张卡的稳定 ID 由 `book-slug + kind + normalized-claim-key` 生成；`normalized-claim-key` 来自稳定的核心命题/方法名，而不是临时措辞、章节号或日期。文件名可读但必须在 manifest 中与 ID 一一映射。重跑时先按稳定 ID、canonical path、ISBN/源文件哈希匹配，再决定 update、merge 或人工冲突；ID 冲突进入 `conflict`，不得自动新建带“新版/副本/2”的文件。
- Wikilink 必须使用当前 vault 可解析的 canonical path，例如 `[[20_Notes/Reading/认知觉醒/概念/注意力.md]]`；同一目录可使用 `[[概念/注意力]]`，但整包应保持一种规范写法。链接目标改名时必须同步修复引用。
- PDF 来源链接使用原附件路径和页码片段，例如 `[[_attachments/Books/example-book.pdf#page=42|PDF p. 42]]`。不要让默认阅读路径或卡片来源链接指向 `90_AI` 中的全文转写。
- `#page=N` 统一表示 PDF 查看器的 1-based 页序；若书内印刷页码不同，在 manifest 或来源审计中另记 `printed_page_label`，不得自行推算偏移。
- 导航页链接入口、首选卡和来源锚点，不复制卡片全文。结构/来源索引可列全量 ID，但默认入口不承担全量索引职责。

## 重跑、更新与冲突

重跑同一本书时：

1. 读取 `90_AI/<book-slug>/manifest.yaml`（或唯一等价的 manifest.json），复用原 `<book-slug>` 与 canonical paths。若 manifest 缺失或版本未知，先扫描 canonical path、书名/ISBN、源文件哈希和卡片稳定 ID；无法唯一匹配时停止写入并报告 `conflict`，不得猜测并新建第二个工作区。
2. 对同 ID 文件执行增量更新，保留用户手工段落（除非用户明确允许覆盖），对来源变化记录 diff/解析损失。
3. 新增卡片放入既有 `概念/`、`方法/` 或必要的 `案例/`；合并重复主题，不在 Reading 根目录建立新文件。
4. 若发现旧的平铺文件，标记为 `legacy/unmigrated` 并在报告中列出，不擅自移动、删除或重命名。
5. 更新入口、问题导航、结构/来源索引和全局索引中的链接，使每个角色仍只有一个 canonical target。

## 布局验收

交付前检查并在报告中给出结果：

- 每本书存在唯一 `20_Notes/Reading/<book-slug>/` 工作区；其入口、问题导航、结构/来源索引和卡片均不在 Reading 根目录平铺。
- 卡片只位于本书的 `概念/`、`方法/`、必要的 `案例/`，或有明确判定的 `30_Knowledge/`；目录深度适中。
- 原始来源位于 `_attachments/Books/`（或已记录的宿主等价位置），必要工作产物位于 `90_AI/<book-slug>/`。PDF direct 模式下无需存在证据层文件。
- `90_AI/<book-slug>/manifest.yaml`（或经声明的唯一等价文件）可被机器读取，且每个逻辑角色都有 canonical path、状态和来源；若生成 AI 说明，则 manifest 的 `canonical.ai_note` 指向唯一的 `<book-title>｜蒸馏说明.md`；没有重复 ID、重复入口或“副本/新版/2”式重跑产物。
- 全局读书索引只指向入口；所有 wikilink 能解析；旧笔记未被未经授权地迁移。
