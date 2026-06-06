# Project Curation Skill Design

**Date:** 2026-06-06

## Goal

Create a reusable skill that helps an agent collect impressive projects from GitHub links or local repository paths, summarize why they are worth saving, and store them in a stable personal knowledge base.

## Inputs

- GitHub repository URL
- Local repository path

## Outputs

- One project note stored at `categories/<category>/<feature>/<project-slug>.md`
- A root `index.md` with bilingual Chinese and English browsing sections
- Optional secondary feature references inside the note body

## Storage Rules

- `index.md` is bilingual: Chinese and English headings, labels, and guidance
- All directories and filenames are English only
- Each project is stored in exactly one primary path
- Extra strengths are recorded as `secondary_features` inside the project note

## Information Model

Each project note should include:

- `title`
- `source_type`
- `repo_url`
- `local_path`
- `category`
- `feature`
- `secondary_features`
- `tags`
- `added_at`
- `status`

Each note body should answer:

- What the project is
- Why it is good
- What implementation ideas are worth borrowing
- Which signals are direct evidence versus inference

## Category and Feature Semantics

- `category` describes the project domain, such as `ai-tools`, `frontend`, `cli`, `infra`
- `feature` describes the standout reason to save it, such as `ux`, `code-architecture`, `performance`, `developer-experience`

## Agent Compatibility

The skill should be usable in three ways:

1. Native Codex skill via `SKILL.md`
2. OpenCode adapter instructions
3. Generic prompt template for other agents

The workflow rules must stay consistent across all three surfaces.

## Workflow

1. Inspect the GitHub repository or local repository
2. Collect high-signal evidence from README, manifests, folder structure, demos, or docs
3. Choose one primary category and one primary feature
4. Create the project note in the canonical path
5. Update the bilingual root `index.md`
6. Mark uncertain judgments as inference

## Initial Scope

The first version is documentation-driven rather than automation-heavy. It provides a strong repeatable workflow, taxonomy guidance, and note templates without requiring custom scripts.
