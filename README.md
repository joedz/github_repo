# 项目索引 / Project Index

| 项目总数 | 已覆盖类别 | 最近更新 | 最近加入 |
|---|---|---|---|
| 8 | 3 | 2026-06-07 | MarkItDown |

## AI 工具 / AI Tools

### 代码理解 / Code Understanding

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [CodeGraph](https://github.com/colbymchenry/codegraph) | 面向 AI coding agents 的本地语义代码图与 MCP 工具层。 | 代码库理解、重构前影响分析、调用链追踪、变更影响测试。 | CLI 安装后执行 `codegraph install` 接入 agent；项目内执行 `codegraph init -i` 建索引。 | 可参考多 agent MCP 接入、安装器配置写入、运行时工具说明注入、本地索引自动同步。 | `mcp` `agent-tooling` `static-analysis` | [查看详情](categories/ai-tools/code-understanding/codegraph.md) |
| [Understand Anything](https://github.com/Lum1104/Understand-Anything) | 多智能体管道分析代码库，构建交互式知识图谱，提供可视化仪表板探索代码结构。 | 代码库理解、引导式浏览、Diff 影响分析、知识图谱构建。 | Claude Code 中 `/plugin marketplace add Lum1104/Understand-Anything` 安装；使用 `/understand` 启动分析。 | 可参考多 Agent 协调模式、知识图谱构建流程、人员适配 UI 设计。 | `knowledge-graph` `code-understanding` `multi-agent` `claude-code-plugin` | [查看详情](categories/ai-tools/code-understanding/understand-anything.md) |

### Agent 运行时 / Agent Runtime

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [ECC](https://github.com/affaan-m/ECC) | 跨 harness 的 agent 运维系统，63 个专用子 agent、251 个技能、79 个命令垫片，覆盖 12 个语言生态。 | Agent 配置与增强、代码审查、安全扫描、多 agent 编排、记忆持久化、验证循环。 | 插件安装：`/plugin marketplace add https://github.com/affaan-m/ECC`；或手动：`./install.sh --profile minimal`。 | 可参考多 harness 兼容层设计、manifest 驱动安装、skill 生命周期、hook 运行时控制。 | `agent` `harness` `workflow` `multi-harness` `skills` `security` | [查看详情](categories/ai-tools/agent-runtime/ecc.md) |

### Agent 编排 / Agent Orchestration

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) | AI coding agent 复利工作流系统，37 skills + 51 agents，支持 10+ 平台。 | 规划→执行→审查→知识沉淀全流程，brainstorm→plan→work→review→compound 循环。 | `/plugin marketplace add` 安装；或 `bunx @every-env/compound-plugin install` 跨平台安装。 | 多 agent 调度架构、manifest 驱动跨平台安装、复利工作流设计、Strategy 锚定模式。 | `agent` `skills` `workflow` `multi-agent` | [查看详情](categories/ai-tools/agent-orchestration/compound-engineering.md) |

### 记忆 / Memory

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [Supermemory](https://github.com/supermemoryai/supermemory) | AI 记忆与上下文引擎，为 AI 应用提供持久化记忆层。 | AI agent/应用的记忆层接入、多轮对话上下文管理、用户偏好持久化、RAG + 个性化上下文混合检索。 | MCP：`npx -y install-mcp@latest https://mcp.supermemory.ai/mcp --client claude --oauth=yes`；npm：`npm install supermemory`。 | 可参考 Memory 引擎设计、混合搜索架构、用户画像分层设计、MCP 协议实现、连接器 webhooks 架构。 | `memory` `rag` `agent-memory` `mcp` `typescript` `postgres` | [查看详情](categories/ai-tools/memory/supermemory.md) |

### Prompt 运维 / Prompt Ops

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [stop-slop](https://github.com/hardikpandya/stop-slop) | 消除 AI 生成文本中“机器味”的 skill 文件。 | 内容创作阶段润色、质量把关阶段 AI 模式过滤、Agent 工具链写作任务接入。 | `npx skills add https://github.com/hardikpandya/stop-slop --skill stop-slop`；或复制 `SKILL.md` 到项目。 | 可参考 Skill 文件结构、评分卡设计、短语黑名单分类组织、trigger 元数据设计、before/after 示例格式。 | `ai-writing` `skill` `content-quality` `prose` `llm` `writing-improvement` | [查看详情](categories/ai-tools/prompt-ops/stop-slop.md) |

## 前端 / Frontend

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [Taste Skill](https://github.com/Leonxlnx/taste-skill) | AI 前端“反垃圾”技能集，提供排版、布局、动效规则，让 AI 生成不再是样板网站。 | 前端实现阶段提供设计规范；设计→代码 pipeline；存量项目 UI 审计与修复。 | `npx skills add https://github.com/Leonxlnx/taste-skill`；或复制 `SKILL.md` 到项目。 | 多专项技能组织方式；三刻度盘参数设计；反套路规则推导；图像→代码两阶段 pipeline；GSAP 动效骨架。 | `agent` `design` `visual-design` `frontend` | [查看详情](categories/frontend/visual-design/taste-skill.md) |

## CLI 工具 / CLI

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [MarkItDown](https://github.com/microsoft/markitdown) | 微软开源的多格式文件转 Markdown CLI 工具，专为 LLM pipeline 设计。 | 文档预处理、文件统一转文本、RAG pipeline 输入。 | `pip install 'markitdown[all]'`；或 Docker。 | Converter 模块分离、插件系统设计、最窄 API 调用规范。 | `markdown` `python` `document-conversion` | [查看详情](categories/cli/documentation/markitdown.md) |
