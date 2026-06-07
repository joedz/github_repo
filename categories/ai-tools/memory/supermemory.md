---
title: "Supermemory"
source_type: github
repo_url: "https://github.com/supermemoryai/supermemory"
local_path: ""
category: ai-tools
feature: memory
secondary_features: ["performance", "extensibility", "api-design", "observability"]
tags: ["memory", "rag", "agent-memory", "mcp", "typescript", "postgres", "cloudflare-workers"]
added_at: 2026-06-07
status: active
---

# Supermemory

## 项目概述

AI 记忆与上下文引擎，为 AI 应用提供持久化记忆层。解决 AI 在对话之间遗忘一切的问题——自动从对话中提取事实、构建用户画像、处理知识更新与矛盾、自动遗忘过期信息，在正确的时间提供正确的上下文。支持完整 RAG、连接器和文件处理，整个上下文栈通过一个 API 提供。

## 特点

- **Memory ≠ RAG**：RAG 检索文档块（无状态，对所有人相同），Memory 提取和追踪用户事实随时间的变化。能理解"我刚搬到 SF"覆盖"我住在 NYC"。
- **混合搜索**：默认 RAG + Memory 合一查询，知识库文档和个性化上下文同时返回。
- **用户画像自动维护**：`profile.static` 长期事实，`profile.dynamic` 近期上下文，单次调用 ~50ms。
- **自动遗忘机制**：临时事实（如"明天有考试"）过期后自动清除；矛盾自动解析；噪声永不变成永久记忆。
- **Benchmarks 第一**：LongMemEval 81.6%（#1）、LoCoMo（#1）、ConvoMem（#1）三个主要 AI memory benchmark 全部第一。
- **多客户端支持**：Claude Desktop、Cursor、Windsurf、VS Code、Claude Code、OpenCode、OpenClaw、Hermes。
- **MCP 服务端开源**：MCP server 源码可查看，可自托管或使用官方托管版本。
- **多框架集成**：Vercel AI SDK、LangChain、LangGraph、OpenAI Agents SDK、Mastra、Agno、Claude Memory Tool、n8n。

## 工作流位置

- AI agent/应用的记忆层接入
- 多轮对话上下文管理
- 用户偏好持久化
- RAG + 个性化上下文混合检索
- AI 工具链的记忆插件（MCP）

## 接入方式

**MCP 快速安装（无需 API key）：**
```bash
npx -y install-mcp@latest https://mcp.supermemory.ai/mcp --client claude --oauth=yes
```
替换 `claude` 为 `cursor`、`windsurf`、`vscode` 等。

**手动 MCP 配置：**
```json
{
  "mcpServers": {
    "supermemory": {
      "url": "https://mcp.supermemory.ai/mcp"
    }
  }
}
```

**npm/pip 安装（开发者 API）：**
```bash
npm install supermemory    # 或：pip install supermemory
```

**框架集成示例（Vercel AI SDK）：**
```typescript
import { withSupermemory } from "@supermemory/tools/ai-sdk";
const model = withSupermemory(openai("gpt-4o"), { containerTag: "user_123", customId: "conv-1" });
```

## 参考方式

- **Memory 引擎设计**：fact extraction、contradiction resolution、temporal-aware forgetting 的实现思路
- **混合搜索架构**：RAG + Memory 在单一查询中的融合方式
- **用户画像抽象**：`profile.static` / `profile.dynamic` 的分层设计
- **MCP 协议实现**：服务端如何暴露 memory/recall/context 工具
- **连接器 webhooks**：外部数据源的实时同步架构
- **Benchmark 框架**：MemoryBench 的标准化评测实现方式

## 简单预览

- 官网：https://supermemory.ai
- Dashboard：https://console.supermemory.ai
- 文档：https://supermemory.ai/docs
- Discord：https://supermemory.link/discord

## 已确认

- 25.9k GitHub stars，2.3k forks
- TypeScript 64.1%、MDX 28.8%、Python 6.2%
- 技术栈：Remix、Tailwind、Vite、Cloudflare Workers/KV/Pages、Drizzle ORM、PostgreSQL
- MCP 服务端开源：https://supermemory.ai/docs/supermemory-mcp/mcp
- 官方提供 app（https://app.supermemory.ai）和 Nova 内置 agent
- 支持的连接器：Google Drive、Gmail、Notion、OneDrive、GitHub、Web Crawler
- 多模态提取：PDFs（OCR）、images（OCR）、videos（transcription）、code（AST-aware chunking）
- 三个 benchmark 第一：LongMemEval 81.6%、LoCoMo、ConvoMem
- MemoryBench 开源，可用于对比 Supermemory、Mem0、Zep 等方案

## 待验证

- 本地 MCP server 部署和自托管流程
- 连接器 webhooks 的实际运行效果
- 在真实 agent 项目中集成 `client.profile()` 的效果
- 多 containerTag 隔离的实际表现

## 备注

与 CodeGraph、Understand Anything、ECC 同属 AI tools 类别，但 Supermemory 定位为记忆层基础设施，而非代码理解或多 agent 编排工具。可作为 AI 应用的 memory backend 接入。
