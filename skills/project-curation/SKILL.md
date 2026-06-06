---
name: project-curation
description: Use when the user wants to save, organize, or review noteworthy software projects from GitHub repository links or local repository paths in a personal library, especially when the collection should be classified by category and standout feature with a bilingual index.
---

# Project Curation

## Overview

Curate saved projects as practical workflow notes, not as loose bookmarks or generic summaries. Every saved project should explain what it is, where it fits into a real development workflow, how to try or integrate it, and which implementation ideas are worth revisiting later.

## Repository Contract

- Store public GitHub project notes at `categories/<category>/<feature>/<project-slug>.md`
- Store local-only project notes at `local_categories/<category>/<feature>/<project-slug>.md`
- Keep all directory names and filenames in English
- Keep the root `index.md` bilingual in Chinese and English
- Keep local-only projects in `index_local.md`, not `index.md`
- Write the project note body in Chinese by default
- Treat `index.md` as a human-facing browsing page, not as a rules manual
- Keep top-of-index helper text minimal; prefer compact stats or other useful overview information
- Give each project exactly one primary storage path
- Record other strengths as `secondary_features` inside the note
- Never commit `index_local.md` or `local_categories/` to a public repository

## Inputs

Accept either:

- a GitHub repository URL
- a local repository path

If both are available, prefer the GitHub URL as the primary source and use the local repository as supporting evidence.

## Public vs Local Routing

Route entries by source type before writing files:

- GitHub repository URL intended for public sharing: update `index.md` and `categories/`
- Local repository path, private project, or locally synchronized fork that should not be published: update `index_local.md` and `local_categories/`

For local entries, the `项目` column may link to a local path or to the user's own remote URL when that helps recognition, but the note file itself must stay under `local_categories/`.

Ensure `.gitignore` includes:

```gitignore
index_local.md
local_categories/
```

## Evidence Collection

Inspect the highest-signal artifacts first:

- `README`
- official docs or website pages inside the repository
- package manifests such as `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`
- visible folder structure
- demo links, screenshots, docs, examples
- installation, deployment, integration, API, CLI, and configuration docs
- local commit history only if it helps clarify intent

If external browsing is available, use primary sources from the repository itself before relying on third-party summaries.

## Classification Rules

Choose:

- one primary `category`: the project domain
- one primary `feature`: the main reason the project deserves saving

Use the taxonomy reference at `references/taxonomy.md` when the classification is ambiguous.

Prefer stable, reusable labels. Do not invent near-duplicates when an existing term already fits.

## Writing Rules

Each note should contain:

1. A short factual summary of what the project does
2. A neutral section describing its main characteristics
3. A section explaining where it fits in a real workflow
4. A section explaining install, deployment, integration, or usage steps when available
5. A section describing implementation ideas worth revisiting
6. A preview section with an image, demo link, or screenshot when available
7. A compact source-notes section for confirmed information and open checks

Use Chinese for section headings and body copy unless the user explicitly asks for another language.

Be specific. "Well structured" is weak. "The CLI keeps command parsing, rendering, and task execution in separate modules" is strong.

Use `已确认` for source-backed facts that support future use. Use `待验证` for local checks, workflow tests, or integration details that still need to be tried.

## Note Template

Start from `templates/project-entry.md`. Fill every field that can be supported by evidence. Leave unavailable fields empty rather than guessing.

Use this frontmatter shape:

```yaml
---
title: ""
source_type: github
repo_url: ""
local_path: ""
category: ""
feature: ""
secondary_features: []
tags: []
added_at: YYYY-MM-DD
status: active
---
```

## Index Update Rules

After writing the note, update the correct index:

- Public entries: `index.md`
- Local-only entries: `index_local.md`

The index should support fast human scanning.

Keep explanation about repository rules minimal inside `index.md`. Put the attention on project summaries and compact overview information.

Organize the index by category. Under each category, use one Markdown table with these columns:

```md
| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [ProjectName](source-link) | 一句话定位 | 它放在开发流程的哪个环节 | 如何安装、部署、嵌入或开始使用 | 可参考的设计、结构或工程化做法 | `tag1` `tag2` | [查看详情](categories/<category>/<feature>/<project-slug>.md) |
```

Write in a neutral tone. Prefer workflow and usage-oriented headings over subjective praise.

In the `项目` column, link to the primary source:

- GitHub URL when the source is a remote repository
- local repository path when the source is local only

For local-only indexes, point `详情` links at `local_categories/<category>/<feature>/<project-slug>.md`.

## Output Path Rules

- Convert the project name to an English slug
- Use lowercase kebab-case for categories, features, and note filenames
- Do not duplicate the same project in multiple primary paths
- Keep public and local paths separate even if the local project is synchronized from GitHub

If a project already exists, update the existing note and index entry instead of creating another copy.

## Cross-Agent Adapters

When the runtime is not Codex-native:

- For OpenCode-specific usage, follow `adapters/opencode.md`
- For other agents, follow `adapters/generic-agent.md`

Those files adapt invocation style only. They do not change the repository contract.
