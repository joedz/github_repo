# 项目索引 / Project Index

This file documents how the generated repository index should be organized.

## Purpose

- Keep the README focused on fast human scanning.
- Surface what is already saved in the collection.
- Avoid showing categories that do not exist in the repository yet.

## Header

At the top of `README.md` and `README_LOCAL.md`, keep a compact stats table such as:

```md
| 项目总数 | 已覆盖类别 | 最近更新 | 最近加入 |
|---|---|---|---|
| 9 | 3 | 2026-06-07 | Headroom |
```

The exact values should be updated from the saved note set.

## Section Generation Rules

- Build category sections from saved note paths under `categories/` or `local_categories/`.
- Render existing categories only.
- Omit empty categories instead of writing placeholder rows.
- Keep public and local indexes separate.
- Within each category, keep one Markdown table for all projects in that category.
- If a category contains meaningful second-level groupings, render those sub-groups explicitly instead of flattening everything into one long table.

## Section Shape

Use bilingual category headings when helpful:

```md
## AI 工具 / AI Tools
```

When a category benefits from a second level, use sub-headings before the tables:

```md
### 代码理解 / Code Understanding
### Agent 运行时 / Agent Runtime
```

Under each category, use this table:

```md
| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [ProjectName](source-link) | 一句话定位 | 它放在开发流程的哪个环节 | 如何安装、部署、嵌入或开始使用 | 可参考的设计、结构或工程化做法 | `tag1` `tag2` | [查看详情](categories/<category>/<feature-or-role>/<project-slug>.md) |
```

For local-only indexes, the `详情` link should point at `local_categories/<category>/<feature-or-role>/<project-slug>.md`.

## Ordering

- Group projects by top-level category first.
- For `ai-tools`, prefer grouping by the second path segment, because that reflects the AI role humans care about when browsing.
- Inside a category, prefer stable ordering such as most recently updated first or alphabetical by project title.
- Keep the ordering rule consistent within the same index.

## Content Rules

- Do not repeat repository policy text in every section.
- Keep tone neutral and workflow-oriented.
- Summaries should help someone decide whether to open the note.
- If a project is classified under `ai-tools`, the detail path should reflect its AI role in the second segment.
