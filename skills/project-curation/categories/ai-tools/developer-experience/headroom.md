---
title: "Headroom"
source_type: github
repo_url: "https://github.com/chopratejas/headroom"
local_path: ""
category: "ai-tools"
feature: "developer-experience"
secondary_features: ["performance"]
tags: ["context-compression", "token-optimization", "mcp", "multi-agent", "claude-code", "proxy", "llm-efficiency"]
added_at: "2026-06-07"
status: "active"
---

# Headroom

## 项目概述

Headroom 是一个面向 AI coding agents 的上下文压缩层，通过多种压缩算法（SmartCrusher、CodeCompressor、Kompress-base）在本地对工具输出、日志、RAG chunks、文件、会话历史等进行预处理后再发送给 LLM，实现 60–95% 的 token 节省，且压缩过程可逆（CCR）。

## 特点

- **多模式接入**：Library（`compress(messages)`）、Proxy（`headroom proxy --port 8787`，零代码改动）、Agent wrap（`headroom wrap claude|codex|cursor|aider|copilot`）、MCP server（`headroom_compress/retrieve/stats`）
- **跨 Agent 记忆共享**：Claude、Codex、Gemini 之间共享压缩上下文，自动去重
- **CCR 可逆压缩**：原始内容不删除，LLM 按需调用 `headroom_retrieve`检索原文
- **CacheAligner 前缀稳定化**：使 provider KV cache 真正命中，而非每次重新计算
- **headroom learn**：从失败会话中挖掘修正模式，自动写入 `CLAUDE.md` / `AGENTS.md` / `GEMINI.md`
- **多内容类型压缩**：SmartCrusher（JSON）、CodeCompressor（AST-aware，Python/JS/Go/Rust/Java/C++）、Kompress-base（HuggingFace 模型，文本）
- **Pipeline 生命周期暴露**：Setup → Pre-Start → Post-Start → Input Received → Input Cached → Input Routed → Input Compressed → Input Remembered → Pre-Send → Post-Send → Response Received，支持 `on_pipeline_event(...)` 扩展
- **Cross-agent memory**：通过 `SharedContext().put / .get` 在多 Agent 工作流间传递压缩上下文

## 工作流位置

- AI coding agent 调用阶段：作为 prompt 前置处理层，减少 token 消耗
- 多 Agent 协作场景：跨 Agent 共享压缩记忆
- Agent 失败分析与改进：`headroom learn` 挖掘失败模式写入项目文档

## 接入方式

```bash
# Python 安装（全部功能）
pip install "headroom-ai[all]"

# Node / TypeScript
npm install headroom-ai

# Docker
docker pull ghcr.io/chopratejas/headroom:latest

# 接入 Claude Code
headroom wrap claude --memory --code-graph

# 零代码改动代理模式
headroom proxy --port 8787

# MCP server模式
headroom mcp install
```

支持 `[proxy]`、`[mcp]`、`[ml]`、`[code]`、`[memory]`、`[relevance]`、`[image]`、`[agno]`、`[langchain]`、`[evals]` 等细粒度安装。

## 参考方式

- **Pipeline 扩展模式**：`on_pipeline_event(...)` 和 compression hooks 的生命周期设计值得在类似中间件中复用
- **多压缩算法路由**：ContentRouter 根据内容类型选择不同压缩器，职责分离清晰
- **Agent wrap 封装**：一行命令完成 agent 环境的代理注入，可参考用于其他 CLI 工具封装
- **Cross-agent memory 共享架构**：SharedContext 的 put/get 设计可用于多 Agent 协作场景
- **可逆压缩实现**：CCR 的原文存储 + 按需检索模式，适用于对精度有要求的压缩场景

## 简单预览

- 官网文档：https://headroom-docs.vercel.app/docs
- Demo GIF：README 中展示了 10,144 → 1,260 tokens 的实际压缩效果
- Kompress-base 模型：https://huggingface.co/chopratejas/kompress-base

## 已确认

- 多语言支持：Python 和 TypeScript/Node 均有官方包
- Python 版本要求：3.10+
- Agent 兼容：Claude Code、Codex、Cursor、Aider、Copilot CLI、OpenClaw
- 协议：Apache 2.0
- 基准测试：在 GSM8K、TruthfulQA、SQuAD v2、BFCL 上验证精度未显著下降
- 压缩可逆：CCR 保证原文不丢失

## 待验证

- Docker 持久化服务配置实际效果
- Windows Credential Manager 认证路径在 Windows 下的实际可用性
- `headroom wrap copilot --subscription` 与 GitHub Copilot CLI 订阅模式的完整集成
- `headroom learn` 在实际项目中的失败挖掘效果
- 与 LangChain、Agno 等框架的深度集成体验