# wow-doc

AI 辅助开发的文档规范管理工具。一键将文档分类和命名规则注入项目，周期性整合清理。

## 设计理念

- **规则注入**：将文档规范写入项目 CLAUDE.md，Claude 自动遵守，无需每次手动调用
- **按类型归类**：spec / api / acceptance / tmp
- **AI 命名**：根据内容自动生成有意义的文件名
- **不限内容**：只管分类和命名，不限制文档内容和结构
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

### 初始化文档规范

在目标项目中执行一次，将文档规范注入项目的 CLAUDE.md：

```
/wow-doc
```

注入后 Claude 会自动遵守文档分类和命名规则，无需再调用此 skill。

### 整理文档

```
/wow-cleanup
```

AI 扫描所有文档，识别重复/过时/碎片文档，向你展示整理建议，确认后执行。

## 文档类型

| 目录 | 用途 |
|------|------|
| `spec/` | 各类分析、方案、实施计划（默认类型） |
| `api/` | API 接口文档 |
| `acceptance/` | 验收标准和结果 |
| `tmp/` | 临时草稿、一次性笔记 |

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
