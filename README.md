# wow-doc

AI 辅助开发的文档按需管理工具。按类型自动归类文档，AI 命名，周期性整合清理。

## 设计理念

从"文档驱动开发"转向"文档辅助开发"：

- **按需生成**：文档是开发过程的自然产物，不是前置条件
- **按类型归类**：spec / api / acceptance / tmp
- **AI 命名**：根据内容自动生成有意义的文件名，不用版本号
- **多版本共存**：同一需求允许多个文档，无需维护唯一活文档
- **周期性整合**：由 AI 主动扫描、合并、归档过时文档

## 安装

```bash
# 推荐：通过 skills CLI
npx skills add zzusp/wow-doc

# 安装指定 skill
npx skills add zzusp/wow-doc --skill wow-doc -g -a claude-code -y

# 手动：复制到 skill 目录
cp -r skills/* ~/.claude/skills/
```

## 使用

### 生成文档

```
/wow-doc 给用户列表增加按作者名搜索功能
```

AI 会自动判断文档类型、生成文件名、写入对应目录。

### 整理文档

```
/wow-cleanup
```

AI 扫描所有文档，识别重复/过时/碎片文档，向你展示整理建议，确认后执行。

## 文档类型

| 目录 | 用途 |
|------|------|
| `spec/` | 需求文档：分析、计划、技术方案，按需自由组织 |
| `api/` | 独立 API 参考文档 |
| `acceptance/` | 验收文档：验收计划和验收结果 |
| `tmp/` | 临时文档：草稿、快速笔记、一次性分析 |

## 目标项目结构

```
your-project/
└── docs/
    ├── spec/
    ├── api/
    ├── acceptance/
    └── tmp/
```

## License

MIT
