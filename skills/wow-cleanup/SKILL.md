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

1. Glob 扫描 `docs/**/*.md` 收集路径
2. 按需读取文件内容用于后续判断（深度自行决定）
3. 必要时通过 git log 获取最后修改时间
4. 形成文档清单：路径、所属类型目录、主题摘要、修改时间

---

## Step 2 — 分析建议

读取 [consolidate.md](consolidate.md) 中的判断维度，对文档清单逐项分析，每个发现的问题生成一条建议，包含：

- 涉及的文档路径
- 问题描述
- 建议的操作（合并 / 归档 / 移动 / 删除）

---

## Step 3 — 用户确认

先调用 `ToolSearch`（query: `"select:AskUserQuestion"`）获取工具 schema。

向用户呈现建议清单并征询处理方式。建议较少时可用 AskUserQuestion 多选；建议较多时先输出文本汇总，让用户按编号筛选或选择批量操作。

用户可以全部接受、逐条选择、全部拒绝，或修改某条建议的操作方式。

---

## Step 4 — 执行整理

按用户确认的建议逐条执行，每条完成后输出结果：

```
✅ 已合并：docs/spec/add-search-filter.md + docs/spec/search-by-author.md → docs/spec/item-list-search-filter.md
✅ 已归档：docs/spec/legacy-auth-flow.md → 并入 docs/spec/auth-overview.md
✅ 已移动：docs/spec/user-module-endpoints.md → docs/api/user-module-endpoints.md
✅ 已删除：docs/tmp/scratch-notes.md（临时文档过期）
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
