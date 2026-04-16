# Skill 编写最佳实践

修改 wow-doc 的 skill 文件前，阅读本文。

## 精简优先

Context window 是公共资源。SKILL.md 加载后每个 token 都与对话历史和其他上下文竞争。

- 只写 Claude 不知道的信息
- 不解释 Claude 已知的概念
- 每段内容都问自己："这值得占 token 吗？"

## 自由度匹配

根据任务的脆弱程度设定指令的精确程度：

- **高自由度**（文本指引）：多种方案都可行时，给方向不给步骤
- **中自由度**（伪代码/参数化）：有推荐模式但允许变化时
- **低自由度**（精确脚本）：操作脆弱、顺序关键时，给具体命令

## 结构规则

- SKILL.md 的 frontmatter 必须包含 `name`（≤64 字符，小写+连字符+数字）和 `description`（≤1024 字符）
- description 用第三人称，包含"做什么"和"什么时候用"
- SKILL.md body 控制在 500 行以内
- 超出时拆分到独立文件，通过链接引用
- 引用层级保持一层：SKILL.md → 子文件，不要 SKILL.md → A.md → B.md
- 超过 100 行的引用文件加目录（TOC）

## 命名

- 全小写 + 连字符：`naming.md`、`error-handling.md`
- 文件名体现内容：`consolidate.md` 而非 `doc2.md`
- 路径用正斜杠：`reference/guide.md` 而非 `reference\guide.md`

## 术语一致性

选定一个术语后全文统一使用。不要混用"文档/doc/文件"、"类型/分类/目录"。

## 迭代验证

修改 skill 逻辑后，用实际场景测试主要路径是否符合预期。
