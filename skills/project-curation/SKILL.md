---
name: project-curation
description: Use when the user wants to save, organize, review, or explicitly reclassify noteworthy software projects from GitHub repository links or local repository paths in a personal library, especially when the collection should be classified by core workflow and indexed for later reuse.
---

# Project Curation

## Overview

Curate saved projects as practical workflow notes, not as loose bookmarks or generic summaries. Every saved project should explain what it is, where it fits into a real development workflow, how to try or integrate it, and which implementation ideas are worth revisiting later.

## Repository Contract

- Generate all indexes and category folders inside the current project root, not inside the source repository being collected and not inside the skill folder.
- Store public GitHub project notes at `<project-root>/categories/<category>/<feature-or-role>/<project-slug>.md`
- Store local-only project notes at `<project-root>/local_categories/<category>/<feature-or-role>/<project-slug>.md`
- Keep all directory names and filenames in English
- Keep public projects in `<project-root>/README.md`
- Keep local-only projects in `<project-root>/README_LOCAL.md`, not `README.md`
- Write the project note body in Chinese by default
- Treat `README.md` and `README_LOCAL.md` as human-facing browsing pages, not as rules manuals
- Keep top-of-index helper text minimal; prefer compact stats or other useful overview information
- Give each project exactly one primary storage path
- Record non-primary strengths as `secondary_features` inside the note
- Never commit `README_LOCAL.md` or `local_categories/` to a public repository

## Inputs

Accept either:

- a GitHub repository URL
- a local repository path

If both are available, prefer the GitHub URL as the primary source and use the local repository as supporting evidence.

## Operating Modes

Support two explicit modes:

- entry curation: add or update one repository note from a GitHub URL or local repository path
- entry reclassification: reorganize already-saved notes under the current taxonomy

Do not enter reclassification mode unless the user explicitly asks to reorganize, reclassify, or re-sort existing entries.

Examples that should trigger reclassification mode:

- "重整现有条目"
- "按新分类规则重分"
- "重新整理 ai-tools"
- "把已有收录重新归类一遍"

Normal add, review, or single-note update requests should stay in entry-curation mode unless the user clearly asks for reclassification.

## Public vs Local Routing

Route entries by source type before writing files:

- GitHub repository URL intended for public sharing: update `<project-root>/README.md` and `<project-root>/categories/`
- Local repository path, private project, or locally synchronized fork that should not be published: update `<project-root>/README_LOCAL.md` and `<project-root>/local_categories/`

For local entries, the `项目` column may link to a local path or to the user's own remote URL when that helps recognition, but the note file itself must stay under `local_categories/`.

Ensure `.gitignore` includes:

```gitignore
README_LOCAL.md
readme_local.md
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

Classify in two stages.

### Stage 1: Choose the Primary Category

Choose exactly one primary `category` based on the repository's core workflow contribution.

Ask:

> Which core development workflow does this repository primarily serve?

Use the taxonomy reference at `references/taxonomy.md` when the classification is ambiguous.

Rules:

- Classify by the job the repository mainly does, not by surface form such as CLI, website, SDK, or plugin.
- Use `ai-tools` only when the repository's main value is serving an AI, agent, model, memory, prompt, evaluation, retrieval, or context workflow.
- If AI is present but not primary, classify by the non-AI workflow instead.
- Prefer stable, reusable labels. Reuse an existing category before creating a new one.

### Stage 2: If Category Is `ai-tools`, Choose the Primary AI Role

If Stage 1 yields `ai-tools`, identify the repository's primary role inside an AI system before choosing the second path segment.

Ask:

> What is this repository mainly responsible for inside an AI system?

Rules:

- Use an existing AI role from `references/taxonomy.md` when one fits.
- Create a new AI role only when no existing role expresses the repository's responsibility without distortion.
- New AI role labels must describe a durable responsibility, not a framework, implementation detail, or marketing phrase.
- Keep the label broad enough that future repositories could reuse it.

For `ai-tools`, the second path segment should usually be the AI role. For non-`ai-tools` categories, the second path segment remains the primary standout feature.

### Secondary Traits

Do not force every good property into the primary path.

- Record other important strengths as `secondary_features`.
- Use tags for additional retrieval hints.
- Keep the primary path focused on one dominant classification.

## Reclassification Mode

When reclassification mode is explicitly requested, reorganize existing notes against the current taxonomy instead of only curating new ones.

### Scope Detection

Support these scopes:

- one project
- one AI role or one sub-group inside a category
- one top-level category such as `ai-tools`
- the whole collection

If the user asks for reclassification but does not clearly specify scope, do not assume a whole-library migration. Prefer the smallest reasonable scope implied by the request.

### Reclassification Flow

For each targeted note:

1. Read the current note and its primary path
2. Re-evaluate the primary `category` from repository evidence and the current taxonomy
3. If the new `category` is `ai-tools`, re-evaluate the primary AI role
4. Compare the current path with the target path
5. Only move the note when the primary path is clearly wrong under the current taxonomy
6. Update note content, tags, and `secondary_features` as needed even if the path does not change

### Migration Rules

- Move the note from the old primary path to the new one when the primary classification changes
- Update the corresponding row in `README.md` or `README_LOCAL.md`
- Do not keep duplicate primary copies in both old and new paths
- Preserve public vs local routing: notes under `categories/` stay public, notes under `local_categories/` stay local

### Deduplication Rules

- A project must have exactly one canonical note
- If the target path already exists for the same project, merge into that note instead of creating a second copy
- Remove old README rows or stale links that would leave the project listed twice

### Stability Rules

- Reclassify only when the main category or main AI role is clearly a better fit under the current taxonomy
- Do not move notes just because wording, tags, or secondary strengths changed
- Be more conservative with path changes than with note-body improvements

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

Interpretation:

- `category`: the core workflow classification
- `feature`: the primary standout feature for non-`ai-tools`, or the primary AI role when `category = ai-tools`
- `secondary_features`: non-primary strengths worth preserving for later retrieval

## Index Update Rules

After writing the note, update the correct README file in the current project root:

- Public entries: `<project-root>/README.md`
- Local-only entries: `<project-root>/README_LOCAL.md`

The index should support fast human scanning.

Keep explanation about repository rules minimal inside README files. Put the attention on project summaries and compact overview information.

Render category sections from the projects that actually exist on disk.

Rules:

- Show only categories that currently have at least one saved note.
- Do not render empty placeholder sections or placeholder-only rows.
- Derive category sections from note paths under `categories/` or `local_categories/`.
- Keep public and local indexes separate even when they contain similar projects.
- During reclassification, remove stale rows from old sections before adding the new row.
- Treat README files as human browsing surfaces first, not as machine dumps.
- For `ai-tools`, do not flatten every project into one long table when the second path segment carries meaningful responsibility.
- Group `ai-tools` entries by human-meaningful responsibility such as AI role, using second-level headings or other clear sub-groups.
- The grouping should make it obvious at a glance what role each AI tool plays in the system.
- If the current AI role list is still too coarse for browsing, introduce a reusable sub-group label rather than hiding the distinction.

Organize the index by category. Under each category, use one Markdown table with these columns:

```md
| 项目 | 定位 | 工作流位置 | 接入方式 | 参考方式 | 标签 | 详情 |
|---|---|---|---|---|---|---|
| [ProjectName](source-link) | 一句话定位 | 它放在开发流程的哪个环节 | 如何安装、部署、嵌入或开始使用 | 可参考的设计、结构或工程化做法 | `tag1` `tag2` | [查看详情](categories/<category>/<feature-or-role>/<project-slug>.md) |
```

Write in a neutral tone. Prefer workflow and usage-oriented headings over subjective praise.

In the `项目` column, link to the primary source:

- GitHub URL when the source is a remote repository
- local repository path when the source is local only

For local-only indexes, point `详情` links at `local_categories/<category>/<feature-or-role>/<project-slug>.md`.

## Output Path Rules

- Convert the project name to an English slug
- Use lowercase kebab-case for categories, features, AI roles, and note filenames
- Do not duplicate the same project in multiple primary paths
- Keep public and local paths separate even if the local project is synchronized from GitHub

If a project already exists, update the existing note and index entry instead of creating another copy.

## Cross-Agent Adapters

When the runtime is not Codex-native:

- For OpenCode-specific usage, follow `adapters/opencode.md`
- For other agents, follow `adapters/generic-agent.md`

Those files adapt invocation style only. They do not change the repository contract.
