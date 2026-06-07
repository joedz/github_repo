---
title: "CodeGraph"
source_type: github
repo_url: "https://github.com/colbymchenry/codegraph"
local_path: ""
category: "ai-tools"
feature: "code-understanding"
secondary_features: ["performance", "code-architecture", "documentation"]
tags: ["mcp", "code-intelligence", "knowledge-graph", "static-analysis", "agent-tooling"]
added_at: 2026-06-06
status: active
---

# CodeGraph

## 项目概述

CodeGraph 是一个面向 AI 编码代理的本地语义代码智能工具。它会为项目建立 `.codegraph/` 本地知识图谱，通过 CLI、MCP server 和 TypeScript API 提供代码搜索、符号关系、调用链、影响分析和上下文构建能力。它支持接入 Claude Code、Cursor、Codex CLI、opencode、Hermes Agent、Gemini CLI、Antigravity IDE 和 Kiro。

## 特点

- 它不是单纯的代码搜索工具，而是把代码库解析成 SQLite 知识图谱：符号、文件、调用关系、依赖关系都可以被 agent 查询。
- 它把多 agent 接入做成了安装器流程，`codegraph install` 会检测目标 agent 并写入 MCP 配置，降低了手动配置成本。
- 它通过 MCP `initialize` 响应给 agent 注入工具使用说明，让 agent 知道什么时候该用 `codegraph_explore`、`codegraph_impact`、`codegraph_callers` 等工具。
- 它考虑了索引新鲜度：文件监听、去抖同步、连接时补同步、staleness banner 都是围绕“不要让 agent 读到过期结构信息”设计的。
- 它既能作为 agent 工具使用，也能作为 TypeScript 库嵌入自己的工具链。

## 工作流位置

- 理解陌生代码库：让 agent 先用 `codegraph_explore` 看结构和关键符号，减少手动 grep/read。
- 重构前评估影响：用 `codegraph_impact` 或 CLI 的 `codegraph impact` 看改动可能影响哪些符号。
- 调试调用链：用 `codegraph_callers`、`codegraph_callees` 或 `codegraph_explore` 追踪入口、处理链和依赖关系。
- 改动后选择测试：用 `codegraph affected` 根据变更文件推导可能受影响的测试文件。
- 多 agent 编码环境：把同一个本地代码图能力接到 Codex、Claude Code、Cursor、opencode 等不同工具里。

## 接入方式

### 安装 CLI

Windows PowerShell：

```powershell
irm https://raw.githubusercontent.com/colbymchenry/codegraph/main/install.ps1 | iex
```

macOS / Linux：

```bash
curl -fsSL https://raw.githubusercontent.com/colbymchenry/codegraph/main/install.sh | sh
```

已有 Node 环境时也可以用 npm：

```bash
npm i -g @colbymchenry/codegraph
```

### 接入 agent

```bash
codegraph install
```

这个步骤负责把 CodeGraph MCP server 接到支持的 agent。README 里还给了非交互用法：

```bash
codegraph install --yes
codegraph install --target=cursor,claude --yes
codegraph install --target=auto --location=local
codegraph install --print-config codex
```

### 初始化具体项目

```bash
cd your-project
codegraph init -i
```

`codegraph init` 创建 `.codegraph/` 目录；加上 `-i` 会同时构建初始索引。之后 agent 启动 MCP server 时，会基于这个本地索引回答代码结构问题。

## 日常使用方式

- 问“这个模块怎么工作”“某个流程从哪里到哪里”时，优先让 agent 使用 `codegraph_explore`。
- 只想找符号位置时，用 `codegraph_search`。
- 查谁调用了某个函数，用 `codegraph_callers`；查某个函数调用了什么，用 `codegraph_callees`。
- 变更前看影响范围，用 `codegraph_impact`。
- 查看索引状态，用 `codegraph_status` 或 CLI 的 `codegraph status`。
- 在命令行脚本或 CI 里，可以用 `git diff --name-only | codegraph affected --stdin --quiet` 找可能受影响的测试。

## 可嵌入方式

CodeGraph 暴露了 TypeScript API，可以直接放进自己的工具或脚本里：

```typescript
import CodeGraph from '@colbymchenry/codegraph';

const cg = await CodeGraph.init('/path/to/project');
await cg.indexAll();

const results = cg.searchNodes('UserService');
const callers = cg.getCallers(results[0].node.id);
const impact = cg.getImpactRadius(results[0].node.id, 2);
const context = await cg.buildContext('fix login bug', {
  maxNodes: 20,
  includeCode: true,
  format: 'markdown',
});

cg.close();
```

可重点关注这些方法：`CodeGraph.init()`、`CodeGraph.open()`、`indexAll()`、`sync()`、`searchNodes()`、`getCallers()`、`getCallees()`、`getImpactRadius()`、`buildContext()`、`watch()`、`close()`。

## 参考方式

- 多 agent 支持：参考 `src/installer/targets/` 下面针对 Claude、Codex、Cursor、opencode、Gemini、Kiro 等 agent 的配置写入方式。
- MCP 工具设计：参考 `src/mcp/tools.ts`、`src/mcp/session.ts`、`src/mcp/server-instructions.ts`，尤其是如何把工具选择策略注入给 agent。
- 本地索引工具：参考 `src/extraction/`、`src/resolution/`、`src/graph/`、`src/search/`、`src/sync/` 的职责拆分。
- 文档组织：参考 `site/src/content/docs/`，它把 quickstart、installation、integrations、API、CLI、MCP server、troubleshooting 拆得比较清楚。
- 工作流产品化：参考它把安装、agent 接入、项目初始化、自动同步、CLI/API/MCP 三种使用方式串成一个完整路径。

## 简单预览

- GitHub：[colbymchenry/codegraph](https://github.com/colbymchenry/codegraph)
- 文档站：[Documentation & Website](https://colbymchenry.github.io/codegraph/)
- 预览图：

![CodeGraph Preview](https://github.com/user-attachments/assets/f168182f-4d9a-44e0-94d7-08d018cc8a3a)

## 已确认

- README 写明安装流程是先安装 CLI，再执行 `codegraph install` 接入 agent，最后在项目内执行 `codegraph init -i`。
- README 和文档站都说明它支持 Claude Code、Cursor、Codex CLI、opencode、Hermes Agent、Gemini CLI、Antigravity IDE 和 Kiro。
- `src/mcp/server-instructions.ts` 显示 MCP server 会在 initialize 阶段向 agent 提供工具使用策略。
- `site/src/content/docs/reference/api.md` 给出了 TypeScript API 的使用方式。
- `src/installer/targets/` 按 agent 拆分配置写入逻辑，说明多 agent 接入是项目的一等能力。
- README 说明索引存储在本地 SQLite 数据库中，并通过文件监听保持更新。

## 待验证

- 在当前 Windows + Codex 环境里实际跑一遍 `codegraph install --print-config codex`，确认生成的 Codex MCP 配置是否符合本机路径。
- 在一个中等规模本地仓库里执行 `codegraph init -i`，记录首次索引耗时和 `.codegraph/` 体积。
- 在实际 Codex 会话中比较一次“有 CodeGraph”和“无 CodeGraph”的代码理解流程，看是否明显减少文件读取。
- 验证 `codegraph affected` 是否能准确匹配当前项目的测试目录命名。

## 备注

这个项目适合作为“agent-native tooling”的参考样板。它值得看的不只是代码分析能力本身，还有它如何把安装器、MCP、运行时说明、本地索引、CLI 和 API 组合成一套可进入日常开发流程的工具。
