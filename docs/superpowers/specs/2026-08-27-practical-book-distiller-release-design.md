# Practical Book Distiller 开源仓库设计

## 目标

将现有 `practical-book-distiller` Codex Skill 打包成一个可公开分发的 GitHub 仓库，服务于“读不完实用书、想先看精华再按需深读”的读者。

## 范围

仓库仅包含通用 Skill、参考文件、安装说明、许可证和版本记录，不包含《认知觉醒》《富爸爸穷爸爸》等个人书摘、PDF、EPUB 或 Obsidian Vault 内容。

## 结构

- `SKILL.md`：Skill 入口和 L0–L5 主流程；
- `references/`：书籍路由、卡片字段、证据政策、导航模板和 Vault 布局；
- `agents/openai.yaml`：Codex 展示信息与自动发现配置；
- `README.md`：中文受众定位、安装、使用和版权说明；
- `CHANGELOG.md`：版本变更；
- `LICENSE`：MIT 许可证；
- `docs/superpowers/specs/`：本次开源打包的设计记录。

## 关键决策

1. 以“按问题快速浏览 + 原文页码回溯”为核心定位，不宣传“完整摘要”或“替代原书”；
2. 对 PDF 默认采用原文件直达模式，不持久化整本文字镜像；
3. 概念卡和方法卡是主要输出，案例卡仅在具有独立迁移价值时创建；
4. README 使用中文，仓库名和 Skill 名使用 `practical-book-distiller`；
5. README 不推荐未经授权的版权下载来源，也不允许上传完整书籍。

## 发布验收

- 所有 Skill 文件来自当前本地版本，未混入个人 Vault 内容；
- README 能说明目标读者、价值、边界、安装和使用方式；
- Markdown 链接、代码块和 YAML 前置元数据格式有效；
- 初始版本标记为 `v0.1.0`；
- GitHub 公开仓库只发布上述开源文件。

