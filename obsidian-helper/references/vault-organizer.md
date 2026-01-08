# Vault Organizer Reference

This reference enables agent skill to organize an Obsidian vault: classify notes, normalize frontmatter, move files, and fix internal links safely (no irreversible deletion, with backups).

## 做什么

- 扫描 vault（排除指定目录）并构建文件清单
- 为笔记补全/规范化 frontmatter（合并模式）
- 依据 `type` 进行分类与移动（默认 Zettelkasten）
- 必要时重命名（仅在确有需要或用户明确要求时）
- 修复内部链接（wikilinks / embeds / markdown links）

## 不做什么（强约束）

- **永不删除**：不做不可逆删除操作
- **organizer 模式下不改写 `.canvas`/`.base`/`.excalidraw.md` 内容**：仅允许移动/重命名；需要改内容必须用户明确提出

# 核心原则（Safety Contract）

- **备份策略**：任何批量变更前，先备份到 `90_Archive/_organizer_backups/`，支持回滚
- **先列清单再执行**：在执行移动/重命名/批量改写前，先输出变更清单（dry-run）给用户确认
- **保守收件箱**：无法确定类型时，笔记保留在 `00_Inbox/`
- **默认排除**：扫描时排除 `90_Archive/`、`99_Plugconfig/`

# 默认目录结构

默认使用 Zettelkasten 目录结构；具体目录定义与 `type -> folder` 映射参考：`references/vault-structure.md`。

# 标准流程（SOP）

## Phase 0：Preflight（预检）

- 确认 vault 根路径与扫描范围
- 读取既有 frontmatter 习惯（是否已经大量存在 `type/tags/aliases`）

产出：扫描/排除规则与风险提示（如重名冲突）

## Phase 1：Backup（备份）

- 创建备份目录：`90_Archive/_organizer_backups/<timestamp>/`
- 将本次变更涉及的文件原样备份（至少包含将被移动/重命名/批量改写的文件）

产出：备份目录路径（用于回滚）

## Phase 2：Inventory（清点）

- 构建文件清单（至少区分 `.md` / `*.excalidraw.md` / `.canvas` / `.base`）
- 标记“不可确定分类”的候选（稍后直接留在 `00_Inbox/`）

产出：inventory 摘要（文件数、类型分布、不确定清单）

## Phase 3：Classify（分类）

分类优先级：

1. 现有 frontmatter `type`
2. 文件当前所在顶层目录（若已在 Zettelkasten 对应目录里，倾向保持）
3. 内容信号（少量启发式；见“分类决策规则”）
4. 兜底：`type: inbox`（放 `00_Inbox/`）

产出：分类映射表（file -> type -> target folder）

## Phase 4：Normalize（frontmatter 规范化）

### Frontmatter schema

```yaml
type: inbox|daily|literature|permanent|map|project|archive
tags: []
aliases: []
```

规则：

- **合并模式**：仅填充缺失字段，保留未知字段
- **tags**：分析内容并添加 3-5 个标签（可去重，但不强行删除用户已有 tags）
- **aliases**：分析内容并添加 1-3 个别名（可去重，但不强行删除用户已有 aliases）

产出：frontmatter 变更清单（哪些文件新增/补齐了哪些字段）

## Phase 5：Move / Rename（移动与重命名）

### 移动策略（默认）

- 默认仅将笔记移动到正确的顶层目录；不做多余的子目录重排
- 如果分类不确定：留在 `00_Inbox/`

### 重命名策略（默认保守）

默认不批量重命名。

只有在以下情况才建议重命名：

- 同目录出现重名冲突需要消解
- 文件名明显无意义且影响检索（例如 `Untitled 3`），并且用户的目标是提高可检索性
- 用户明确指定命名规则

产出：move/rename 变更清单

## Phase 6：Link Fix + Verify（修链接与验证）

### 链接修复范围

重命名/移动时自动修复：

- Wikilinks：`[[...]]`
- Embeds：`![[...]]`
- Markdown 链接：`[](...)`

### 验证要求

- 抽样检查：移动/重命名后的目标文件仍可被引用解析
- 输出无法自动修复的链接清单（如目标缺失、歧义匹配）

产出：验证摘要（修复数量、剩余问题、回滚路径）

# 分类决策规则（简版）

- `daily`：明显的日记/日期驱动记录（或原本位于 `01_Daily/`）
- `literature`：读书笔记/文献摘录/引用整理（或原本位于 `10_Literature/`）
- `project`：围绕具体交付目标的项目资料/任务推进（或原本位于 `40_Projects/`）
- `map`：索引/MOC/导航页，用于组织链接（或原本位于 `30_Maps/`）
- `permanent`：可复用的沉淀知识、概念总结（或原本位于 `20_Permanent/`）
- 不确定：`inbox`
