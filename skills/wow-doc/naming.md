# 命名规则

## 核心原则

**文件名即内容摘要。** 读文件名就能知道文档在讲什么。

---

## 规则

1. **语言**：英文、全小写、连字符分隔
2. **长度**：3-6 个词，短而清晰
3. **结构**：`<主题>-<限定词>.md`
4. **不重复类型**：目录已表达类型，文件名不再重复（`spec/` 下不要叫 `xxx-spec.md`）

---

## 命名示例

| 类型 | 好的命名 | 差的命名 | 原因 |
|------|---------|---------|------|
| spec | `user-search-by-author.md` | `spec-1.md` | 无内容信息 |
| spec | `order-export-batch.md` | `order-export-spec.md` | 重复类型 |
| api | `user-module-endpoints.md` | `api-doc.md` | 重复类型且模糊 |
| acceptance | `item-list-filter-assertions.md` | `test.md` | 太模糊 |
| acceptance | `order-export-round2-results.md` | `acceptance-1.md` | 无内容信息 |
| tmp | `tech-stack-notes.md` | `temp.md` | 太模糊 |

---

## 冲突处理

当目标目录下已有同名文件时：

1. **内容属于同一主题的演进** → 直接更新该文件（覆盖写入）
2. **内容确实不同** → 用限定词区分，体现内容差异：
   - `user-auth-jwt-approach.md` vs `user-auth-session-approach.md`
   - `order-export-csv-format.md` vs `order-export-excel-format.md`

**判断方法：** 读取已有文件的标题和前 20 行，与当前要写入的内容比对。主题相同则更新，主题不同则用限定词区分。
