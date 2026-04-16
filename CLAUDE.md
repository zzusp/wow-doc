# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

本仓库是一套可安装的 **Agent Skills**（`npx skills add zzusp/wow-doc`），不是业务项目。包含两个 skill：

- **wow-doc** — 按需生成文档，自动分类到 spec/api/acceptance/tmp，AI 根据内容命名
- **wow-cleanup** — 扫描 `docs/` 识别重复/过时/碎片文档，用户确认后整合清理

核心原则：**只管分类和命名，不限制文档内容和结构。**

## Repository Structure

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

## Architecture

wow-doc SKILL.md 是主入口，包含完整工作流（Step 0 → Step 1 → Step 2）和四类文档的分类判断要点。naming.md 和 error-handling.md 通过链接按需加载（一层引用，不嵌套）。

wow-cleanup SKILL.md 定义扫描→建议→确认→执行的流程，consolidate.md 定义具体的合并/归档/移动/删除策略。consolidate.md 通过 `../wow-doc/SKILL.md` 和 `../wow-doc/naming.md` 跨 skill 引用分类和命名规则。

## Editing Rules

- 修改任何 skill 文件前，先阅读 `reference/best-practices.md`
- skill 文件保持精简：不解释 Claude 已知的常识，只写 Claude 没有的上下文
- 文件命名：全小写 + 连字符（如 `naming.md`、`error-handling.md`）
- 不在 skill 文件里硬编码用户项目的具体路径
- SKILL.md body 控制在 500 行以内，超出时拆分到独立文件
- 引用层级保持一层：SKILL.md → 子文件，不要 A.md → B.md → C.md
