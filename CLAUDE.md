# CLAUDE.md — wow-doc

本仓库是一套可安装的 **Agent Skills**，不是业务项目。在此仓库中工作时请遵守以下规则。

## 仓库结构

```
skills/
  wow-doc/             # 按需生成文档 skill
    SKILL.md           # 入口（含分类规则和写入逻辑）
    naming.md          # 命名规则
    error-handling.md  # 异常处理
  wow-cleanup/         # 文档整合清理 skill
    SKILL.md           # 入口
    consolidate.md     # 合并/归档逻辑
reference/
  best-practices.md    # Skill 编写参考指南，修改 skill 前必读
```

## 编写规则

- 修改任何 skill 文件前，先阅读 `reference/best-practices.md`
- skill 文件保持精简：不解释 Claude 已知的常识，只写 Claude 没有的上下文
- 文件命名：全小写 + 连字符（如 `naming.md`、`error-handling.md`）
- 不在 skill 文件里硬编码用户项目的具体路径
- SKILL.md body 控制在 500 行以内，超出时拆分到独立文件
