---
name: wow-cleanup
description: 整理和合并项目文档：扫描 docs/ 目录，识别重复、过时或碎片化文档，向用户展示整理建议，确认后执行合并、归档、重分类或删除操作。
disable-model-invocation: true
---

# /wow-cleanup — 文档整合清理

扫描项目 `docs/` 下所有文档，识别可整理项，用户确认后执行。

```
全量扫描 → 分析建议 → 用户确认 → 执行整理
```

合并/归档逻辑详见 [consolidate.md](consolidate.md)。

---

## Step 1 — 全量扫描

1. 使用 Glob 扫描 `docs/**/*.md`，收集所有文档路径
2. 读取每个文件的标题（`# ` 开头行）和前 20 行内容
3. 获取每个文件的最后修改时间（通过 `git log -1 --format=%ci <file>` 或文件系统时间）
4. 构建文档清单：路径、所属类型目录、主题摘要、最后修改时间

---

## Step 2 — 分析建议

读取 [consolidate.md](consolidate.md) 中的判断规则，对文档清单执行以下分析：

| 检查项 | 说明 |
|--------|------|
| 重复文档 | 同一类型目录下主题高度重叠的多个文档 |
| 过时文档 | 引用了已不存在的代码/接口/文件 |
| 碎片文档 | 同一主题的信息分散在多个小文档中 |
| 错误归类 | 文档内容与所在类型目录不匹配（spec/api/acceptance/tmp） |
| 空文档 | 内容不足 5 行的文档 |
| tmp 过期 | `tmp/` 下超过一定时间未更新的临时文档 |

对每个发现的问题，生成一条建议，包含：
- 涉及的文档路径
- 问题描述
- 建议的操作（合并/归档/移动/删除）

---

## Step 3 — 用户确认

先调用 `ToolSearch`（query: `"select:AskUserQuestion"`）获取工具 schema。

**如果建议数量 ≤ 4**，使用 `AskUserQuestion` 的 multiSelect 模式，让用户勾选要执行的建议。

**如果建议数量 > 4**，分批展示，每批最多 4 条。或者以文本形式列出所有建议，让用户逐条确认/拒绝。

用户可以：
- 全部接受
- 逐条选择
- 全部拒绝
- 修改某条建议的操作方式

---

## Step 4 — 执行整理

按用户确认的建议逐条执行，每条完成后输出结果：

```
✅ 已合并：docs/spec/add-search-filter.md + docs/spec/search-by-author.md → docs/spec/item-list-search-filter.md
✅ 已归档：docs/spec/old-payment-analysis.md → docs/_archive/old-payment-analysis.md
✅ 已移动：docs/spec/user-module-endpoints.md → docs/api/user-module-endpoints.md
✅ 已删除：docs/tmp/scratch-notes.md（临时文档清理）
```

全部完成后输出整理报告摘要：

```
📋 整理完成
   合并：X 组
   归档：X 个
   移动：X 个
   删除：X 个
   未变更：X 个
```
