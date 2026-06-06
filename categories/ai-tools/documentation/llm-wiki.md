---
title: "llm-wiki"
source_type: github
repo_url: "https://github.com/Pratiyush/llm-wiki"
local_path: ""
category: "ai-tools"
feature: "documentation"
secondary_features: ["cli", "knowledge-management", "ai-exports"]
tags: ["wiki", "knowledge-base", "session-history", "static-site", "ai-agent", "claude-code", "codex", "cursor", "obsidian"]
added_at: 2026-06-07
status: active
---

# llm-wiki

## 项目概述

将 AI 编程助手（Claude Code、Codex CLI、Copilot、Cursor、Gemini CLI）的对话记录自动转化为可搜索、互相链接的个人知识库。基于 Andrej Karpathy 的 LLM Wiki 模式构建，输出静态站点和 AI 可消费的导出格式。

## 特点

- **多适配器会话同步**：自动检测并导入 Claude Code、Codex CLI、Cursor、Gemini CLI、Obsidian 等多个 AI 编程工具的会话记录
- **Karpathy 双层架构**：Layer 1 将 jsonl 会话转为原始 markdown；Layer 2 通过 AI 生成 wiki 页面（sources/entities/concepts/syntheses/comparisons/questions）
- **丰富的 AI 可消费导出**：每个 HTML 页面都有 `.txt`、`.json` 同级文件，另有 `llms.txt`、`llms-full.txt`、`graph.jsonld`、`sitemap.xml`、`rss.xml` 等站点级入口
- **本地静态站点**：Python stdlib + markdown 构建，无需数据库或 npm，CDN 加载 highlight.js 实现语法高亮
- **Obsidian 原生集成**：提供 link-obsidian CLI 将 wiki 符号链接到 Obsidian vault，支持 Dataview 查询和 Templater 模板
- **质量治理体系**：4 因子置信度评分、5 状态生命周期（draft→reviewed→verified→stale→archived）、16 条 lint 规则（含 LLM 驱动规则）
- **MCP 服务器**：12 个生产级工具（query/search/list/read/lint/sync/export + confidence/lifecycle/dashboard/entity search/category browse）可通过 MCP 客户端调用

## 工作流位置

- **个人知识管理**：将散落的 AI 会话记录转化为结构化文档
- **代码理解**：通过 wiki 形式回顾之前 AI 辅助开发的技术决策和实现细节
- **AI 工具链**：作为 AI agent 的知识查询端点，其他 AI 可通过 llms.txt 或 graph.jsonld 查询项目历史

## 接入方式

```bash
# 克隆仓库
git clone https://github.com/Pratiyush/llm-wiki.git
cd llm-wiki

# macOS/Linux
./setup.sh

# Windows
setup.bat

# 基本使用
llmwiki init    # 一次性脚手架，创建 raw/、wiki/、site/ 目录
llmwiki sync    # 同步会话并构建 wiki
llmwiki build   # 编译静态 HTML
llmwiki serve   # 本地预览 http://127.0.0.1:8765

# 一站式构建
llmwiki all     # build + graph + export + lint

# 可选：pip 安装
pip install -e .                    # 基础版
pip install -e '.[graph]'           # + graphify AI 图谱引擎
pip install -e '.[all]'             # graph + 所有可选依赖
```

## 参考方式

- **多适配器架构**：adapters 目录下每个 AI 工具独立适配器，标准化会话导入接口，适合扩展新数据源
- **双层知识组织**：Layer 1 保持原始会话 immutable，Layer 2 通过 AI 生成结构化 wiki，职责分离清晰
- **AI 可消费导出设计**：每个页面附带 `.txt`/`.json` sibling，站点级提供 llms.txt 和 graph.jsonld，适合作为 AI agent 的知识查询后端
- **质量治理模式**：置信度评分 + 生命周期状态机 + 16 条 lint 规则的组合，可迁移到其他需要维护内容质量的系统
- **无服务器静态站点**：纯 Python stdlib + markdown 生成静态 HTML，部署简单（GitHub Pages、Docker、Nix flakes 均有支持）

## 简单预览

- 官网 Demo：https://pratiyush.github.io/llm-wiki
- 构建演示：70 秒 CLI 教程视频见 `docs/demo.gif`
- 截图包括：项目概览 + 活动热力图、会话列表、session 详情页、changelog 渲染、项目索引等

## 已确认

- 基于 Karpathy 的 LLM Wiki pattern（原始 gist：https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f）
- 支持 Claude Code、Codex CLI、Copilot、Cursor、Gemini CLI、Obsidian 六个数据源适配器
- 输出格式：HTML + `.txt` + `.json` sibling per page、站点级 llms.txt、llms-full.txt、graph.jsonld、sitemap.xml、rss.xml、robots.txt、ai-readme.md、manifest.json
- 静态站点功能：全局搜索（Cmd+K fuzzy match）、highlight.js 语法高亮（暗色/亮色主题）、键盘快捷键、`[[wikilinks]]` 互相链接、活动热力图、模型信息卡、vs-comparison 页面
- 依赖：Python 3.9+，纯 stdlib + markdown，无 npm 或数据库依赖
- 部署方式：Docker、docker-compose、GitHub Pages、flake.nix

## 待验证

- `SessionStart` hook 自动同步功能（需在 ~/.claude/settings.json 中配置）
- `--synthesize` 选项调用本地 Claude/Ollama 生成概述页面的实际效果
- `--vault` 选项将 wiki 写入 Obsidian/Logseq vault overlay 的体验
- MCP 服务器在实际 MCP 客户端（Claude Desktop、Cline、Cursor）中的查询体验

## 备注

- 450 commits，293 stars，45 forks，活跃项目
- v1.3.8，MIT license
- CI 完善：CI、link-check、wiki-checks、Docker build 均通过