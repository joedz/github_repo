# Taxonomy Reference

Use stable English labels for directories and filenames. Keep the actual saved path compact and predictable.

## Core Workflow Categories

Choose the primary category by the repository's core workflow contribution, not by its surface form.

| Chinese | English slug | Use for |
|---|---|---|
| AI 工具 | `ai-tools` | Repositories whose main value serves AI, agent, model, memory, prompt, retrieval, evaluation, or context workflows |
| 前端 | `frontend` | Web UI, component systems, visualization, and design-heavy product surfaces |
| CLI 工具 | `cli` | Terminal tools, shell workflows, and command-line developer automation |
| 基础设施 | `infra` | Deployment, DevOps, platform engineering, observability, and runtime operations |
| 后端 | `backend` | APIs, services, server frameworks, and data-processing backends |
| 数据工具 | `data-tools` | ETL, analytics tooling, data pipelines, and data applications |
| 移动端 | `mobile` | iOS, Android, React Native, and Flutter applications |
| 游戏 | `games` | Game engines, game tooling, and interactive play experiences |
| 自动化 | `automation` | Bots, browser automation, workflow automation, and task runners where AI is not the primary workflow |
| 教育 | `education` | Learning products, teaching tools, and study systems |

## AI Role Suggestions

If `category = ai-tools`, the second path segment should describe the repository's primary role inside an AI system.

Choose the closest reusable role first.

| Chinese | English slug | Use for |
|---|---|---|
| 代码理解 | `code-understanding` | Codebase analysis, structural exploration, semantic code graphs, and repository understanding for AI systems |
| Agent 运行时 | `agent-runtime` | Execution environments, harnesses, wrappers, and runtime layers for agents |
| Agent 编排 | `agent-orchestration` | Multi-agent coordination, routing, task decomposition, and workflow orchestration |
| 上下文工程 | `context-engineering` | Context shaping, compression, prompt pre-processing, and context routing |
| 记忆 | `memory` | Persistent memory, preference storage, temporal knowledge, and recall layers |
| 评估 | `evaluation` | Eval harnesses, scoring systems, benchmarks, and regression-quality loops |
| Prompt 运维 | `prompt-ops` | Prompt management, versioning, prompt deployment, and prompt workflow governance |
| 工具接入 | `tool-integration` | MCP layers, connectors, tool bridges, and external capability integration |
| 知识摄取 | `knowledge-ingestion` | Document loading, parsing, normalization, and ingestion into AI systems |
| 知识检索 | `knowledge-retrieval` | Search, retrieval, ranking, and retrieval augmentation layers |
| 开发体验 | `developer-experience` | Local setup, packaging, scaffolding, docs, onboarding, and operator ergonomics for AI tooling |
| 交互界面 | `interface` | Human-facing UI surfaces for interacting with AI systems |

These are not a closed list. Add a new AI role only when an existing one does not fit.

## Non-AI Feature Suggestions

For categories other than `ai-tools`, the second path segment should usually capture the main standout feature.

| Chinese | English slug | Use for |
|---|---|---|
| 交互体验 | `ux` | Flow design, polished interactions, clarity, and delight |
| 代码结构 | `code-architecture` | Module boundaries, layering, and maintainable structure |
| 工程化 | `developer-experience` | Tooling, setup quality, docs, scaffolding, and local workflow |
| 性能优化 | `performance` | Rendering speed, memory efficiency, and runtime optimization |
| 视觉设计 | `visual-design` | Typography, layout, styling, and visual identity |
| API 设计 | `api-design` | Clean interfaces, composability, and SDK ergonomics |
| 可扩展性 | `extensibility` | Plugin systems, hooks, and customization surfaces |
| 测试质量 | `testing` | Strong test coverage, test ergonomics, and reliability patterns |
| 可观测性 | `observability` | Logging, tracing, dashboards, and diagnostics |
| 文档表达 | `documentation` | Clear docs, examples, onboarding, and teaching quality |

Use these as secondary traits too when they are important but not primary enough to drive the path.

## New Label Rules

Create a new category or AI role only when all of the following are true:

1. No existing label fits without distortion.
2. The new label describes a durable responsibility or workflow, not an implementation detail.
3. The label is broad enough that future projects could plausibly reuse it.
4. The label is not a near-duplicate of an existing term.

Avoid labels such as:

- technology-specific names like `langchain-tools`
- vague labels like `awesome-ai`
- one-off labels like `meeting-summary-agent`

If you add a new AI role, add it to this file with a short explanation so later classifications stay consistent.

## Tie-Breaking

If multiple top-level categories fit, choose the one that best matches the repository's core workflow contribution.

If `ai-tools` fits, ask which responsibility the repository mainly serves inside an AI system and use that AI role as the second path segment.

If multiple features or AI roles still fit, choose the label you would most likely use to find the project again six months later.
