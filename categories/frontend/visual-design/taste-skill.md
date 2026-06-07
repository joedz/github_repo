---
title: "Taste Skill"
source_type: github
repo_url: "https://github.com/Leonxlnx/taste-skill"
local_path: ""
category: "frontend"
feature: "visual-design"
secondary_features: ["ux"]
tags: ["agent", "design", "ai", "frontend", "skills", "codex", "claude", "claude-code"]
added_at: 2026-06-07
status: active
---

# Taste Skill

## 项目概述

Taste Skill 是一个面向 AI 编码代理的"反垃圾"前端设计技能集。通过可移植的 SKILL.md 文件，为 AI agent 提供排版、布局、动效和间距的设计规则，使 AI 生成的前端不再停留在"样板网站"水平。包含多个专项技能（代码实现类）和图像生成技能（参考图类），可搭配 ChatGPT Images、Codex、Cursor 或 Claude Code 使用。

## 特点

- 主技能 `design-taste-frontend`（v2）通过三个可调节参数（DESIGN_VARIANCE / MOTION_INTENSITY / VISUAL_DENSITY，范围1-10）控制输出风格。
- 包含10 个专项技能，覆盖绿色场景（taste-skill）、GPT/Codex 严格模式（gpt-taste）、图像优先工作流（image-to-code-skill）、存量项目审计（redesign-skill）、柔和高端风格（soft-skill）、编辑类产品风格（minimalist-skill）、硬核野兽派（brutalist-skill）、Google Stitch 兼容（stitch-skill）、完整输出强制（output-skill）。
- 三个图像生成技能（imagegen-frontend-web、imagegen-frontend-mobile、brandkit）生成设计参考图，输出给编码 agent 实现。
- 硬性规则：禁止 em-dash（—），要求标准 GSAP 代码骨架，设计系统映射，pre-flight 检查协议。
- 框架无关：不绑定 React/Vue/Svelte，规则面向设计意图而非框架 API。
- 通过 `npx skills add`接入 Vercel Agent Skills CLI，所有技能统一管理。

## 工作流位置

- 前端实现阶段：给 AI agent 提供设计规范，让它生成不再是"Generic Bootstrap UI"的前端代码。
- 设计→代码 pipeline：先用 imagegen 技能生成参考图，feed 给 Codex/Cursor/Claude Code 实现。
- 存量项目改造：用 redesign-skill 先审计 UI，再按 layout、spacing、hierarchy、styling 逐一修复。
- 输出质量控制：output-skill 解决 agent 总是截断输出、交付半成品的问题。

## 接入方式

### 安装全部技能

```bash
npx skills add https://github.com/Leonxlnx/taste-skill
```

### 安装单个技能

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
npx skills add https://github.com/Leonxlnx/taste-skill --skill "gpt-taste"
npx skills add https://github.com/Leonxlnx/taste-skill --skill "image-to-code"
npx skills add https://github.com/Leonxlnx/taste-skill --skill "redesign-existing-projects"
```

### 手动使用

直接复制 `skills/` 下的 `SKILL.md` 到项目中，或粘贴到 ChatGPT / Codex 对话里。

### 在 AI Agent 中触发

以 Codex 为例，在会话中说明使用哪个技能：

```
follow the skill: generate images, then analyze, then code
```

或直接附加 imagegen 技能生成的参考图，然后请求实现。

## 参考方式

- **多专项技能组织**：参考它把一个设计目标拆成10+ 个独立 SKILL.md 的方式，每个技能只做一件事，可按需组合。
- **可调节参数设计**：三个1-10 刻度盘（VARIANCE / MOTION / DENSITY）让 agent 在统一框架内输出风格可调的输出，而不是非此即彼的开关。
- **反垃圾规则**：参考 `research/` 下的背景研究，理解"AI 生成界面为什么容易看起来廉价"，以及针对性的规则设计。
- **图像→代码 pipeline**：imagegen-frontend-web / mobile 生成参考图，image-to-code-skill 做图像分析再转代码，两阶段设计值得迁移。
- **GSAP 动效骨架**：taste-skill v2 提供了 canonical GSAP 代码模板，包含了 scroll、magnetic、hover 等场景的标准写法。

## 简单预览

-官网：[tasteskill.dev](https://tasteskill.dev)
- 示例站点（用 taste-skill 构建）：[Floria](https://github.com/Leonxlnx/taste-skill/blob/main/examples/floria-top.webp)
- 预览图：

![Taste Skill Banner](https://github.com/Leonxlnx/taste-skill/raw/main/assets/readme-banner.png)

## 已确认

- README 说明接入方式是 `npx skills add https://github.com/Leonxlnx/taste-skill`，支持 Vercel Labs 的 agent-skills CLI。
- README 明确列出支持 Codex、Cursor、Claude Code 三个主要 AI 编码工具。
- skills/ 目录下有 10 个代码实现技能 + 3 个图像生成技能，文件夹名即技能名。
- taste-skill v2 默认安装名为 `design-taste-frontend`，同时提供 pinning用的 `design-taste-frontend-v1`。
- README 说明 SKILL.md 是 portable instruction file，可通过 CLI 安装或直接复制到项目/对话中使用。
- 35.4k stars、2.6k forks、MIT license、97 commits。
- research/ 目录包含背景研究文档，说明反垃圾设计规则的推导过程。
- CHANGELOG.md 记录了 v1 到 v2 的完整 diff 和重写原因。

## 待验证

- 在 Codex 或 Claude Code 会话中实际使用 `design-taste-frontend` 技能，确认输出前端质量与默认生成的差异。
- 测试 `image-to-code-skill` 的完整 pipeline：生成参考图 → 分析 → 代码实现。
- 验证三个参数刻度盘（1-10）在实际项目中是否真的有可感知的风格差异。
- 在一个实际前端项目中用 redesign-skill 审计现有 UI 并逐一修复，记录改进效果。

## 备注

Taste Skill 的核心价值不在于某个具体规则，而在于它把"什么是好的前端设计"翻译成了 AI agent 可以执行的指令。它值得参考的是：如何把设计决策变成可调节的参数、如何组织多专项技能让 agent 按需选用、如何通过 research/ 建立反垃圾设计的理论基础。