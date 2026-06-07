---
title: "Compound Engineering"
source_type: github
repo_url: "https://github.com/EveryInc/compound-engineering-plugin"
local_path: ""
category: ai-tools
feature: agent-orchestration
secondary_features: ["agent", "multi-agent", "skills", "workflow", "code-review", "debugging"]
tags: ["agent", "skills", "workflow", "multi-agent", "claude-code-plugin", "codex", "copilot"]
added_at: 2026-06-07
status: active
---

# Compound Engineering

## 项目概述

AI 技能与 agent 系统，通过"复利工程"理念让每次开发工作都为后续工作积累优势。核心循环为：brainstorm → plan → work → review → compound，形成知识复利。已适配 Claude Code、Codex、Cursor、Copilot、Droid、Qwen Code、OpenCode、Pi、Gemini、Kiro 等多平台。

## 特点

- **37 个 skill 和 51 个 agent**，覆盖规划、审查、调试、记忆等多个维度
- **多平台统一插件系统**：通过 Bun/TypeScript 安装器实现跨平台适配，各平台 manifest 驱动
- **复利工作流**：每个环节的输出（brainstorm 文档、plan 方案、review 反馈）作为下一环节的输入，逐步积累上下文
- **策略锚定**：`/ce-strategy` 维护 `STRATEGY.md`，为后续所有环节提供产品背景 grounding
- **`/ce-compound` 知识固化**：将失败教训和成功经验文档化，供未来 agent 复用，避免重复踩坑
- **多 agent 协调模式**：`$ce-code-review`、`$ce-plan`、`$ce-work` 等技能调度专用子 agent 执行并行任务

## 工作流位置

- **规划阶段**：`/ce-brainstorm` 交互式需求梳理 → `/ce-plan` 实现方案制定
- **执行阶段**：`/ce-work` 通过 worktree 执行计划，支持任务跟踪
- **审查阶段**：`/ce-code-review` 多 agent 代码审查
- **知识沉淀**：`/ce-compound` 将本次经验固化为可复用文档
- **产品信号**：`/ce-product-pulse` 生成时间窗口内的用户反馈与产品表现报告

## 接入方式

### Claude Code

```text
/plugin marketplace add EveryInc/compound-engineering-plugin
/plugin install compound-engineering
```

### Codex

```bash
codex plugin marketplace add EveryInc/compound-engineering-plugin
bunx @every-env/compound-plugin install compound-engineering --to codex
# 然后在 Codex TUI 中 /plugins 安装 compound-engineering
```

### GitHub Copilot (VS Code / CLI)

```text
/ plugin marketplace add EveryInc/compound-engineering-plugin
/plugin install compound-engineering@compound-engineering-plugin
```

### OpenCode

```bash
bunx @every-env/compound-plugin install compound-engineering --to opencode
```

### 本地开发

```bash
# 添加 shell alias
alias cce='claude --plugin-dir ~/Code/compound-engineering-plugin/plugins/compound-engineering'

# 或使用本地 CLI
bun run src/index.ts install ./plugins/compound-engineering --to opencode
```

## 参考方式

- **跨平台插件 manifest 设计**：各平台 `plugin.json` 统一格式，通过转换器适配不同平台的插件系统
- **多 agent 调度架构**：`$ce-code-review` 等技能通过 subagent 工具派发并行任务到专门的 reviewer/researcher agent
- **Skill 生命周期管理**：安装时写入 skill 目录，cleanup 时自动备份旧 artifact，防止 stale 安装
- **复利工作流设计**：brainstorm → plan → work → review → compound 循环，每个环节的输出物自动流入下一环节
- **Bun 作为跨平台安装工具**：一个 CLI驱动多平台安装，通过 `--to` 参数选择目标，避免为每个平台维护独立安装脚本
- **Strategy 锚定模式**：`STRATEGY.md` 作为所有规划活动的 grounding，上下文字段流动到 brainstorm、plan 等文档

## 简单预览

- [Full component reference](https://github.com/EveryInc/compound-engineering-plugin/blob/main/plugins/compound-engineering/README.md)
- [Compound Engineering: how Every codes with agents](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents)
- [The story behind compounding engineering](https://every.to/source-code/my-ai-had-already-fixed-the-code-before-i-saw-it)

## 已确认

- 37 skills + 51 agents库存（已确认自 README）
- 支持平台：Claude Code, Codex, Cursor, Copilot, Droid, Qwen Code, OpenCode, Pi, Gemini, Kiro（已确认自 README）
- MIT license（已确认自 LICENSE）
- 由 [@kieranklaassen](https://github.com/kieranklaassen) 和 [@tmchow](https://github.com/tmchow)维护（已确认自 README Contributing 部分）
- 核心循环：brainstorm → plan → work → review → compound（已确认自 README Philosophy 部分）
- 通过 `bunx @every-env/compound-plugin`转换器实现跨平台安装（已确认自 README）

## 待验证

- 本地安装到 OpenCode 并验证 skill 是否正常加载
- `/ce-compound` 生成的笔记在后续项目中是否真正被复用
- 与现有 stop-slop、ECC 等 agent 系统共存时的优先级/冲突处理
- Codex 平台在 agent 步骤和 skill 步骤分离维护的未来演进路径

## 备注

与 stop-slop（AI 写作质量）不同，Compound Engineering 定位是 AI coding agent 的**工作流编排与知识复利**，是 agent 工具链的骨架系统而非单点技能。
