# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

本仓库是一套可安装的 **Agent Skills**（`npx skills add zzusp/wow-doc`），不是业务项目。包含两个 skill：

- **wow-doc** — 初始化文档规范，将分类和命名规则注入目标项目的 CLAUDE.md，一次性操作
- **wow-cleanup** — 扫描 `docs/` 识别重复/过时/碎片文档，用户确认后整合清理

## Repository Structure

```
skills/
  wow-doc/             # 文档规范初始化 skill
    SKILL.md           # 入口（注入规则到目标项目 CLAUDE.md）
  wow-cleanup/         # 文档整合清理 skill
    SKILL.md           # 入口
    consolidate.md     # 合并/归档逻辑
reference/
  best-practices.md    # Skill 编写参考指南，修改 skill 前必读
```

## Architecture

wow-doc SKILL.md 是单文件 skill，工作流为：定位 CLAUDE.md → 检查是否已有规则 → 追加规则块 → 确认。无子文件引用。

wow-cleanup SKILL.md 定义扫描→建议→确认→执行的流程，consolidate.md 定义具体的合并/归档/移动/删除策略。

## Editing Rules

- 修改任何 skill 文件前，先阅读 `reference/best-practices.md`
- skill 文件保持精简：不解释 Claude 已知的常识，只写 Claude 没有的上下文
- 文件命名：全小写 + 连字符（如 `consolidate.md`、`best-practices.md`）
- 不在 skill 文件里硬编码用户项目的具体路径
- SKILL.md body 控制在 500 行以内，超出时拆分到独立文件
- 引用层级保持一层：SKILL.md → 子文件，不要 A.md → B.md → C.md
