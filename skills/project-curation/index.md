# 项目索引 / Project Index

| 项目总数 | 已覆盖类别 | 最近更新 | 最近加入 |
|---|---|---|---|
| 9 | 3 | 2026-06-07 | Headroom |

## AI 工具 / AI Tools

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [CodeGraph](https://github.com/colbymchenry/codegraph) | 面向 AI coding agents 的本地语义代码图与 MCP 工具层。 | 代码库理解、重构前影响分析、调用链追踪、变更影响测试。 | CLI 安装后执行 `codegraph install` 接入 agent；项目内执行 `codegraph init -i` 建索引。 | 可参考多 agent MCP 接入、安装器配置写入、运行时工具说明注入、本地索引自动同步。 | `mcp` `agent-tooling` `static-analysis` | [查看详情](categories/ai-tools/developer-experience/codegraph.md) |
| [Understand Anything](https://github.com/Lum1104/Understand-Anything) | 多智能体管道分析代码库，构建交互式知识图谱，提供可视化仪表板探索代码结构。 | 代码库理解、引导式浏览、Diff 影响分析、知识图谱构建。 | Claude Code 中 `/plugin marketplace add Lum1104/Understand-Anything` 安装；使用 `/understand` 启动分析。 | 可参考多 Agent 协调模式、知识图谱构建流程、人员适配 UI 设计。 | `knowledge-graph` `code-understanding` `multi-agent` `claude-code-plugin` | [查看详情](categories/ai-tools/code-architecture/understand-anything.md) |
| [ECC](https://github.com/affaan-m/ECC) | 跨 harness 的 agent 运维系统，63 个专用子 agent、251 个技能、79 个命令垫片，覆盖 12 个语言生态。 | Agent 配置与增强、代码审查、安全扫描、多 agent 编排、记忆持久化、验证循环。 | 插件安装：`/plugin marketplace add https://github.com/affaan-m/ECC`；或手动：`./install.sh --profile minimal` | 可参考多 harness 兼容层设计、manifest 驱动安装、skill 生命周期、hook 运行时控制。 | `agent` `harness` `workflow` `multi-harness` `skills` `security` | [查看详情](categories/ai-tools/developer-experience/ecc.md) |
| [Supermemory](https://github.com/supermemoryai/supermemory) | AI 记忆与上下文引擎，为 AI 应用提供持久化记忆层，自动提取事实、构建用户画像、处理知识更新与矛盾、自动遗忘过期信息。 | AI agent/应用的记忆层接入、多轮对话上下文管理、用户偏好持久化、RAG + 个性化上下文混合检索。 | MCP：`npx -y install-mcp@latest https://mcp.supermemory.ai/mcp --client claude --oauth=yes`；npm：`npm install supermemory`；MCP 手动配置或 API key 接入。 | 可参考 Memory 引擎设计（fact extraction、contradiction resolution、temporal forgetting）、混合搜索架构、用户画像分层设计、MCP 协议实现、连接器 webhooks 架构。 | `memory` `rag` `agent-memory` `mcp` `typescript` `postgres` | [查看详情](categories/ai-tools/developer-experience/supermemory.md) |
| [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) | AI coding agent 复利工作流系统，37 skills + 51 agents，支持 10+ 平台。 | 规划→执行→审查→知识沉淀全流程，brainstorm→plan→work→review→compound 循环。 | `/plugin marketplace add` 安装；或 `bunx @every-env/compound-plugin install` 跨平台安装。 | 多 agent 调度架构、manifest 驱动跨平台安装、复利工作流设计、Strategy 锚定模式。 | `agent` `skills` `workflow` `multi-agent` | [查看详情](categories/ai-tools/developer-experience/compound-engineering.md) |
| [stop-slop](https://github.com/hardikpandya/stop-slop) | 消除 AI 生成文本中"机器味"的 skill 文件，通过短语黑名单、公式化结构规则和 5 维度评分卡去除 throat-clearing、被动语态、模糊表述等 AI tells。 | 内容创作阶段润色、质量把关阶段 AI 模式过滤、Agent 工具链写作任务接入。 | `npx skills add https://github.com/hardikpandya/stop-slop --skill stop-slop`；或复制 SKILL.md 到项目；或将 SKILL.md 包含在 system prompt 中。 | 可参考 Skill 文件结构（SKILL.md + references/ 分离）、评分卡设计（5 维度 + 阈值）、短语黑名单分类组织、trigger 元数据设计、before/after 示例格式。 | `ai-writing` `skill` `content-quality` `prose` `llm` `writing-improvement` | [查看详情](categories/ai-tools/ux/stop-slop.md) |
| [Harness](https://github.com/revfactory/harness) | Claude Code 的 meta-skill，自动将领域描述生成为 agent 团队和技能，支持 6 种团队架构模式。 | 复杂任务分解、agent 团队自动配置、多 agent 协作流程设计。 | `/plugin marketplace add revfactory/harness` + `/plugin install harness@harness`；或复制 `skills/harness` 到 `~/.claude/skills/harness`。 | 可参考 6 种预定义 agent 团队架构模式、渐进式技能生成、inter-agent 编排协议设计。 | `claude-code` `claude-code-plugin` `harness` `multi-agent` `agent-team` | [查看详情](categories/ai-tools/developer-experience/harness.md) |
| [Headroom](https://github.com/chopratejas/headroom) | AI coding agents 的上下文压缩层，60–95% token 节省，支持多 Agent记忆共享和 CCR 可逆压缩。 | AI agent 调用阶段作为 prompt 前置处理层；多 Agent 协作场景共享压缩记忆；`headroom learn` 挖掘失败模式。 | `pip install "headroom-ai[all]"` 安装；`headroom wrap claude` 封装 agent；`headroom proxy --port 8787` 零代码改动代理；MCP：`headroom mcp install`。 | Pipeline 扩展模式（on_pipeline_event）、多压缩算法路由设计（ContentRouter）、Agent wrap 封装、Cross-agent memory 共享架构。 | `context-compression` `token-optimization` `mcp` `multi-agent` `llm-efficiency` | [查看详情](categories/ai-tools/developer-experience/headroom.md) |

## 前端 / Frontend

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [Taste Skill](https://github.com/Leonxlnx/taste-skill) | AI 前端"反垃圾"技能集，提供排版/布局/动效规则，让 AI 生成不再是样板网站。 | 前端实现阶段提供设计规范；设计→代码 pipeline；存量项目 UI 审计与修复。 | `npx skills add https://github.com/Leonxlnx/taste-skill`；或复制 SKILL.md 到项目。 | 多专项技能组织方式；三刻度盘参数设计；反垃圾规则推导；图像→代码两阶段 pipeline；GSAP 动效骨架。 | `agent` `design` `visual-design` `frontend` | [查看详情](categories/frontend/visual-design/taste-skill.md) |

## CLI 工具 / CLI

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| 暂无 | - | - | - | - | - | - |

## 基础设施 / Infrastructure

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| 暂无 | - | - | - | - | - | - |

## 后端 / Backend

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| 暂无 | - | - | - | - | - | - |

## 数据工具 / Data Tools

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| 暂无 | - | - | - | - | - | - |

## 移动端 / Mobile

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| 暂无 | - | - | - | - | - | - |

## 游戏 / Games

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| 暂无 | - | - | - | - | - | - |

## 自动化 / Automation

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| 暂无 | - | - | - | - | - | - |

## 教育 / Education

| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| 暂无 | - | - | - | - | - | - |
