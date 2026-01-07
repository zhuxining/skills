---
name: obsidian-organizer
description: 整理和规范化 Obsidian 笔记库（Zettelkasten 风格）。支持文件重命名、移动、frontmatter 补全、链接修复等操作。
---

# 核心原则

- **永不删除**：不做不可逆删除操作
- **备份策略**：执行前备份到 `90_Archive/_organizer_backups/`，支持回滚
- **保守收件箱**：无法确定类型时，笔记保留在 `00_Inbox`

# 笔记库结构（Zettelkasten）

## 顶层文件夹

- `00_Inbox/`
- `01_Daily/`
- `10_Literature/`
- `20_Permanent/`
- `30_Maps/`
- `40_Projects/`
- `90_Archive/`
- `99_Plugconfig/`

## 附件管理

同级目录下固定的 `_assets/` 子文件夹存放附件（如有）

# 文件处理规则

## Frontmatter 规则

```yaml
type: inbox|daily|literature|permanent|map|project|archive
tags: []
aliases: []
```

规则：

- **合并模式**：仅填充缺失字段，保留未知字段
- **tags**：分析内容并添加3-5个标签
- **aliases**：分析内容并添加1-3个别名

## 链接修复

重命名/移动时自动修复：

- Wikilinks：`[[...]]`
- Markdown 链接：`[](...)`

# 扫描范围

默认排除：`90_Archive/`、`99_Plugconfig/`

## 特殊文件类型

- `*.excalidraw.md`：视为 Markdown，可重命名/移动/合并 frontmatter
- `*.canvas` 和 `*.base`：可重命名/移动，不重写内容

# Trigger phrases / intents (examples)

当用户要求扫描/组织黑曜石保险库时使用此技能，特别是：

- “帮我整理一下 Obsidian vault / 笔记库”
- “把文件名统一成 YYYYMMDD\_标题”
- “批量补全/规范 frontmatter”
