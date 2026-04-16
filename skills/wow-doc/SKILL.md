---
name: wow-doc
description: 初始化项目文档规范：将文档分类和命名规则写入目标项目的 CLAUDE.md。一次性操作，执行后可卸载此 skill。
disable-model-invocation: true
---

# /wow-doc — 文档规范初始化

将文档分类和命名规则注入到当前项目的 CLAUDE.md 中。执行一次即可。

```
定位 CLAUDE.md → 检查是否已有规则 → 追加规则块 → 确认
```

---

## Step 1 — 定位 CLAUDE.md

在当前工作目录根目录查找 CLAUDE.md：
- 存在 → 继续 Step 2
- 不存在 → 创建空文件，继续 Step 2

## Step 2 — 检查是否已有规则

读取 CLAUDE.md 全文，判断是否已包含文档分类规范（spec/api/acceptance/tmp）：
- 已包含 → 告知用户规则已存在，结束
- 未包含 → 继续 Step 3

## Step 3 — 追加规则块

在 CLAUDE.md 末尾追加：

~~~markdown
## 文档规范

在 `docs/` 下按类型归档（目录不存在时按需创建）：
- `spec/` — 各类分析、方案、实施计划（默认类型）
- `api/` — API 接口文档
- `acceptance/` — 验收标准和结果
- `tmp/` — 临时草稿、一次性笔记

命名：英文全小写 + 连字符，3-6 词，内容即名称，不在文件名中重复目录类型。
~~~

## Step 4 — 确认

输出：

```
✅ 文档规范已注入：CLAUDE.md
   Claude 将自动遵守这些规则，无需再调用 /wow-doc。
```
