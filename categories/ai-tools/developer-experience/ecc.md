---
title: "ECC"
source_type: github
repo_url: "https://github.com/affaan-m/ECC"
local_path: ""
category: ai-tools
feature: developer-experience
secondary_features: ["security", "multi-harness", "skills-system", "memory-persistence", "continuous-learning"]
tags: ["agent", "harness", "workflow", "multi-harness", "skills", "security", "llm"]
added_at: 2026-06-07
status: active
---

# ECC

## 项目概述

ECC（Evolved Coding Companion）是一个面向 AI coding agents 的 harness 原生运维系统，跨 Codex、Claude Code、Cursor、OpenCode、Gemini、Zed、GitHub Copilot 等主流 harness 运行。提供 63 个专用子 agent、251 个技能、79 个遗留命令垫片，以及 hooks、rules、MCP 配置的完整体系。10+ 个月真实产品开发迭代沉淀，支持多语言规则（TypeScript、Python、Go、Java、Perl、C++、Rust 等 12 个语言生态）。

## 特点

- **跨 harness 一致性**：同一套 agents、skills、hooks、rules 同时支持 Claude Code 插件安装、Codex CLI、Cursor、OpenCode、Zed、Gemini 等多个 harness，行为对齐。
- **分层架构**：agents/（子 agent 委托）、skills/（工作流定义）、hooks/（生命周期自动化）、rules/（always-follow 规范）、commands/（slash 命令兼容层）清晰分离。
- **选择性安装**：manifest 驱动的安装管道，`install-plan.js` + `install-apply.js` 支持细粒度组件安装，state store 跟踪已安装内容实现增量更新。
- **安全内建**：AgentShield 集成 `/security-scan` skill，1282 测试用例、102 条规则覆盖主流攻击向量。
- **Rust 控制平面原型**：ECC 2.0 alpha 在 `ecc2/` 目录下构建，本地可用暴露 `dashboard`、`start`、`sessions`、`status`、`stop`、`resume`、`daemon` 命令。
- **记忆持久化**：hooks 实现 session 跨启停自动保存/加载上下文，配合 strategic-compact 自动压缩建议。
- **持续学习**：Instinct-based learning with confidence scoring，支持 import/export/evolution 将 session 模式提取为可复用技能。

## 工作流位置

- **Agent 配置与增强**：为 AI coding agent 提供预制的 skills、rules、hooks 系统。
- **代码审查**：多语言 reviewer agent（TypeScript、Python、Go、Java、C++、Rust、Kotlin 等）+ security-reviewer。
- **构建错误修复**：各语言 build-resolver agent 自动定位并修复编译错误。
- **安全扫描**：集成 AgentShield 的 `/security-scan` skill。
- **多 agent 编排**：`multi-plan`、`multi-execute`、`multi-backend`、`multi-frontend`、`multi-workflow` 命令族。
- **记忆与上下文管理**：session 生命周期 hooks 自动持久化，context 压缩优化。
- **验证循环**：checkpoint vs continuous eval，grader types，pass@k metrics。

## 接入方式

```bash
# 插件安装（推荐）
/plugin marketplace add https://github.com/affaan-m/ECC
/plugin install ecc@ecc

# 手动安装
git clone https://github.com/affaan-m/ECC.git
cd ECC && npm install
./install.sh --profile minimal --target claude

# 仪表盘 GUI
npm run dashboard
# 或
python3 ./ecc_dashboard.py
```

安装后可通过 `/ecc:plan "task"` 使用 namespaced 命令，或直接用 `/plan`、`/code-review` 等短形式（手动安装路径）。

## 参考方式

- **多 harness 兼容层设计**：同一套配置如何通过 plugin manifest、install 脚本、state store 实现跨 7+ harness 一致行为。
- **选择性安装架构**：`install-plan.js` manifest 驱动、`install-apply.js` 增量应用、SQLite state store 跟踪的完整实现。
- **子 agent 委托模式**：`agents/` 目录下 63 个专用 agent 的 prompt 结构和委托边界设计。
- **Skill 生命周期**：skill 创建、版本化、导出/导入、evolution clustering 的完整流程（`/skill-create`、`/evolve`）。
- **Hook 运行时控制**：`ECC_HOOK_PROFILE`、`ECC_DISABLED_HOOKS` 等环境变量实现 hook 严格程度动态切换。
- **Instinct 学习系统**：confidence scoring、import/export、evolution 将零散 session 模式组织为可复用技能的工作流。

## 简单预览

暂无（可参考 [ECC Dashboard 截图](assets/images/guides/shorthand-guide.png) 或社交媒体上的 guide 图片）

## 已确认

- 182K+ stars，28K+ forks，170+ 贡献者，MIT 许可证。
- 63 agents、251 skills、79 legacy command shims，覆盖 TypeScript、Python、Go、Java、Perl、C++、Rust、Kotlin、Swift、PHP 等 12 个语言生态。
- npm 包 `ecc-universal`（周下载量）、`ecc-agentshield`；GitHub App `ecc-tools`（150+ 安装）。
- 997+ 内部测试全部通过（v1.8.0）。
- `ecc2/` Rust 原型支持 dashboard/start/sessions/status/stop/resume/daemon 命令。
- 支持环境变量控制 hook 严格程度（`ECC_HOOK_PROFILE`、`ECC_DISABLED_HOOKS`）。
- NanoClaw v2 实现 model routing、skill hot-load、session branch/search/export/compact/metrics。
- 5-layer guard 防止 observer loop。

## 待验证

- 在真实 Claude Code 项目中安装并使用 `/plan` 和 `/security-scan` 的体验。
- `multi-*` 命令族的实际多 agent 编排效果（需额外安装 `ccg-workflow` 运行时）。
- ECC Pro ($19/seat/mo) 私人仓库 GitHub App 的具体功能差异。
- Rust `ecc2/` 控制平面从 alpha 到 general release 的进展。

## 备注

- OSS 永远免费，ECC Pro 是私人仓库的托管 GitHub App 变现方式。
- 建议先从 minimal profile 开始安装，避免一次性加载过多 context。