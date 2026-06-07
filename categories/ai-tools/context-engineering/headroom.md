---
title: Headroom
source_type: github
repo_url: https://github.com/chopratejas/headroom
local_path: ""
category: ai-tools
feature: context-engineering
secondary_features: ["memory", "tool-integration"]
tags: ["context-compression", "token-optimization", "mcp", "proxy", "agent-tooling", "python", "typescript"]
added_at: 2026-06-07
status: active
---

# Headroom

## 项目概览

Headroom 是一个 AI agent 的上下文压缩层，通过 6 种算法（CacheAligner、ContentRouter、SmartCrusher、CodeCompressor、Kompress-base、IntelligentContext）将 tool 输出、日志、RAG chunks、文件和对话历史压缩 60–95% 后再发送给 LLM，同时保留可逆性（CCR）。支持 Python/TypeScript 库、代理模式、MCP 服务器和主流 coding agent（Claude Code、Codex、Cursor、Aider、Copilot）的一键包装。

## 特点

- **多算法协同压缩**：SmartCrusher 压缩 JSON、CodeCompressor 做 AST 感知的代码压缩、Kompress-base 基于 HuggingFace 模型压缩文本、IntelligentContext 做基于评分的重要性排序。
- **CacheAligner**：稳定前缀，使 provider KV cache 真正命中。
- **CCR 可逆压缩**：原始内容永不删除，LLM 通过 `headroom_retrieve` 按需检索。
- **跨 agent 记忆**：共享存储、agent 来源追踪、自动去重，支持 Claude、Codex、Gemini 之间共享上下文。
- **`headroom learn`**：挖掘失败 session，将修正写入 `CLAUDE.md` / `AGENTS.md` / `GEMINI.md`。
- **多接入模式**：库模式（`compress(messages)`）、代理模式（零代码改动）、agent wrap 模式、MCP 服务器模式。
- **多框架兼容**：Anthropic SDK、OpenAI SDK、Vercel AI SDK、LiteLLM、LangChain、Agno、Strands。

## 工作流位置

- **上下文压缩**：在 tool 输出 / RAG 结果到达 LLM 之前做预处理
- **Token 成本优化**：减少 60–95% 的 token 消耗
- **跨 agent 记忆共享**：多 agent 协作时的一致性上下文
- **失败学习**：从错误中提取模式并写入项目规范

## 接入方式

```bash
# Python
pip install "headroom-ai[all]"

# Node / TypeScript
npm install headroom-ai

# Docker
docker pull ghcr.io/chopratejas/headroom:latest

# Agent wrap（Claude Code、Codex、Cursor 等）
headroom wrap claude

# 代理模式（零代码改动）
headroom proxy --port 8787

# MCP 工具安装
headroom mcp install
```

按需安装子模块：`[proxy]`、`[mcp]`、`[ml]`（Kompress-base）、`[code]`、`[memory]`、`[relevance]`、`[image]`、`[agno]`、`[langchain]`、`[evals]`。要求 Python 3.10+。

## 参考方式

- **多算法路由架构**：ContentRouter 检测内容类型选择合适压缩器，职责分离清晰
- **Pipeline 生命周期设计**：Setup → Post-Start → Input Cached → Input Routed → Input Compressed → Pre-Send → Post-Send → Response Received，transform 和 extension 解耦
- **MCP 工具层实现**：`headroom_compress`、`headroom_retrieve`、`headroom_stats` 三个核心工具的接口设计
- **跨 agent 共享内存**：SharedContext 的 put/get 设计，支持多 agent 协作
- **可逆压缩实现**：CCR 通过 `headroom_retrieve` 按需还原，原始内容本地持久化

## 简单预览

- 文档：https://headroom-docs.vercel.app/docs
- PyPI：https://pypi.org/project/headroom-ai/
- npm：https://www.npmjs.com/package/headroom-ai
- Kompress-base 模型：https://huggingface.co/chopratejas/kompress-base

压缩效果 demo（10,144 → 1,260 tokens，92% 压缩率）：https://raw.githubusercontent.com/chopratejas/headroom/main/HeadroomDemo-Fast.gif

## 已确认

- Apache 2.0 许可证
- Python 3.10+ 和 TypeScript 支持
- 支持的 agent：Claude Code、Codex、Cursor、Aider、Copilot CLI、OpenClaw
- 基准测试：GSM8K（数学）±0.000 精度保持、TruthfulQA（事实）+0.030、SQuAD v2 97%、BFCL 工具 97%
- 实际工作负载压缩率：代码搜索 92%、SRE 事故调试 92%、GitHub issue 分类 73%、代码库探索 47%
- 跨平台：Linux/macOS/Windows、Docker 支持

## 待验证

- 本地代理模式在 Windows Credential Manager 的认证复用（文档提到但未完全验证）
- `[image]` 压缩模块的实际效果
- `headroom learn` 在长期使用中的失效模式挖掘质量
- 与 LangChain / Agno 集成的生产级稳定性

## 备注

- RTK 作为 shell 输出重写的底层工具被集成在 Headroom 依赖中
- 支持 GitHub Copilot CLI 订阅模式通过 `headroom wrap copilot --subscription`