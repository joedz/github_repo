---
title: "Harness"
source_type: github
repo_url: "https://github.com/revfactory/harness"
local_path: ""
category: ai-tools
feature: developer-experience
secondary_features: ["multi-agent", "claude-code-plugin", "skills", "agent-team"]
tags: ["claude-code", "claude-code-plugin", "harness", "harness-engineering", "multi-agent", "agent-team"]
added_at: 2026-06-07
status: active
---

# Harness — Agent Team & Skill Architect

## 项目概述

Harness 是一个 Claude Code 插件（meta-skill），通过一句话描述即可自动生成领域专属的 agent 团队和技能。它将复杂任务分解为协调的专业化 agent，自动生成 `.claude/agents/` 中的 agent 定义和 `.claude/skills/` 中的技能文件。

## 特点

- **6 种团队架构模式**：Pipeline（流水线）、Fan-out/Fan-in（发散-收敛）、Expert Pool（专家池）、Producer-Reviewer（生产者-审查者）、Supervisor（监督者）、Hierarchical Delegation（层级委托）
- **渐进式披露技能生成**：Auto-generates skills with Progressive Disclosure for efficient context management
- **编排协议**：内置 inter-agent 数据传递、错误处理和团队协调协议
- **验证机制**：触发验证、dry-run 测试、with-skill vs without-skill 对比测试
- **性能验证**：A/B 测试显示质量评分提升 +60%，复杂任务 100% 胜率

## 工作流位置

- **复杂任务分解**：将多步骤复杂任务自动分配给专业化 agent 团队
- **Agent 工具链配置**：为 Claude Code 项目生成专用多 agent 工作流
- **团队架构设计**：提供预定义的 6 种团队协作模式，适用于不同复杂度的任务

## 接入方式

```shell
# 方式一：通过 marketplace 安装（推荐）
/plugin marketplace add revfactory/harness
/plugin install harness@harness

# 方式二：直接复制 skills 目录
Copy the `skills/harness` directory to `~/.claude/skills/harness`
```

安装后只需说：
- English: "build a harness for this project"
- 한국어: "하네스 구성해줘"
- 日本語: "ハーネスを構成して"

## 参考方式

- **Agent 团队架构设计**：6 种预定义模式可直接迁移到其他 agent 框架
- **渐进式技能生成**：Progressive Disclosure 模式可用于组织复杂技能的上下文管理
- **多 agent 编排协议**：inter-agent 数据传递和协调模式可作为其他系统的参考实现
- **Harness-100 衍生项目**：100 个生产级 agent 团队 harness，可直接用于 10 个领域的任务

## 简单预览

- 官网：https://revfactory.github.io/harness/
- 演示截图：https://github.com/revfactory/harness（项目页面）
- GitHub Stars: 6,262

## 已确认

- 6 种团队架构模式均已实现并文档化
- 支持多语言触发：英语、韩语、日语
- Apache License 2.0 开源协议
- 衍生项目 harness-100 提供 100 个生产级 agent 团队（10 个领域，200 个包，1,808 个文件）
- 相邻项目：coleam00/Archon（运行时配置工厂）、SaehwanPark/meta-harness（Codex 移植版）、affaan-m/ECC（跨 harness 标准化层）

## 待验证

- 在实际 Claude Code 项目中触发 "build a harness for this project" 的生成效果
- 验证生成的 agent 定义和技能文件在实际任务中的协作效果
- 测试 6 种架构模式在不同复杂度任务下的表现差异
- 对比 with-skill vs without-skill 的实际质量提升

## 备注

- L3 Meta-Factory 层工具，定位于"生成其他 harness 的工厂"
- 与 Archon 同属 L3 层，Archon 负责运行时配置确定性，Harness 负责团队架构生成
