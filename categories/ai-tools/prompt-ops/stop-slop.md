---
title: "stop-slop"
source_type: github
repo_url: "https://github.com/hardikpandya/stop-slop"
local_path: ""
category: "ai-tools"
feature: "prompt-ops"
secondary_features: ["documentation", "developer-experience"]
tags: ["ai-writing", "skill", "content-quality", "prose", "llm", "writing-improvement"]
added_at: 2026-06-07
status: active
---

# stop-slop

## 项目概述

一个用于消除 AI 生成文本中"机器味"的 skill 文件。通过结构化的规则库和短语黑名单，帮助 LLM 识别并移除 AI 写作中的典型模式，包括填充短语、公式化结构、被动语态、模糊表述等，让 prose 读起来更像人类写作。已获 3K stars。

## 特点

- **多层规则体系**：分为短语规则（phrases）、结构规则（structures）、句级规则三层，层层递进
- **量化评分卡**：5 维度评分（直接性、节奏、信任度、真实感、密度），总分低于 35/50 则需修订
- **具体黑名单**：在 `references/phrases.md` 中列出具体要删除的短语（如 "Here's what"，所有副词），而非泛泛建议
- **转换示例**：在 `references/examples.md` 中提供 before/after 对比，直观展示修改效果
- **7 条核心规则**：Cut filler phrases、Break formulaic structures、Use active voice、Be specific、Put the reader in the room、Vary rhythm、Trust readers
- **快速检查清单**：交付前逐项检查 adverbs、passive voice、inanimate verbs、Wh- 开头等14 项

## 工作流位置

- **内容创作阶段**：AI 生成初稿后，作为编辑/润色工具介入
- **质量把关阶段**：在 prose交付前进行 AI 模式过滤
- **Agent 工具链**：作为 skill 接入 Claude Code 等 AI 编码 agent，在写作任务中自动触发

## 接入方式

**Claude Code**：
```
将 stop-slop 文件夹添加为 skill
```

**npx 安装**：
```
npx skills add https://github.com/hardikpandya/stop-slop --skill stop-slop
```

**自定义指令**：复制 `SKILL.md` 中的核心规则到 system prompt
**API 调用**：将 `SKILL.md` 包含在 system prompt 中，reference 文件按需加载

## 参考方式

- **Skill 文件结构**：`SKILL.md` + `references/` 分离核心规则与详细数据库，可复用到其他领域（如代码审查、设计点评）
- **评分卡设计**：5 维度量化评分 + 阈值判断，可迁移到其他质量评估场景
- **短语黑名单组织**：分类存储（throat-clearing、emphasis crutches、business jargon、adverbs），方便针对性启用/禁用子集
- **Before/After 示例模式**：在 `references/examples.md` 中展示转换效果，适合作为其他内容质量工具的参考格式
- **Trigger 元数据设计**：`SKILL.md` 中 `trigger` 字段定义触发场景，实现 skill 的按需激活

## 简单预览

暂无官方截图或 demo 页面。可通过 GitHub README 或 `skills.sh`（`https://skills.sh/hardikpandya/stop-slop/stop-slop`）查看内容。

## 已确认

- 项目由 Hardik Pandya 开发，采用 MIT 许可证
- 目录结构：`SKILL.md` + `references/phrases.md` + `references/structures.md` + `references/examples.md`
- 支持 Claude Code skill格式接入
- 3K stars（截至 2026-01-11），表明社区认可度高
- 规则覆盖广度：14+ 类 throat-clearing phrases、50+  business jargon 替换表、所有 -ly 副词
- 规则粒度：从短语级别（"Here's what"）到句式级别（Wh- 开头、em-dash）到风格级别（被动语态、模糊表述）

## 待验证

- 在实际项目中接入 Claude Code，验证 skill 触发和规则生效情况
- 测试对复杂 prose（如技术文档、多段落 essay）的修正效果
- 评估 5 维度评分卡的可操作性和阈值合理性
- 验证 `npx skills add` 安装方式在本地环境的兼容性

## 备注

与 Taste Skill（`frontend/visual-design/taste-skill`）同属 AI "反垃圾"工具集，但 domain 不同：Taste Skill 针对前端/设计输出，stop-slop 针对 prose写作输出。两者可互补，构成 AI 生成内容的全面质量过滤体系。
