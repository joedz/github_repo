# Project Curation Skill Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a reusable cross-agent skill for collecting and indexing noteworthy software projects from GitHub URLs or local repository paths.

**Architecture:** Store the core workflow in one Codex-style skill folder and add lightweight supporting files for taxonomy, note templates, and adapter guidance for OpenCode and generic agents. Keep the repository output format stable so any agent can follow the same convention.

**Tech Stack:** Markdown, repository conventions, agent skill metadata

---

### Task 1: Create planning and skill directories

**Files:**
- Create: `docs/superpowers/specs/2026-06-06-project-curation-skill-design.md`
- Create: `docs/superpowers/plans/2026-06-06-project-curation-skill.md`
- Create: `skills/project-curation/SKILL.md`
- Create: `skills/project-curation/agents/openai.yaml`
- Create: `skills/project-curation/templates/project-entry.md`
- Create: `skills/project-curation/references/taxonomy.md`
- Create: `skills/project-curation/adapters/opencode.md`
- Create: `skills/project-curation/adapters/generic-agent.md`
- Create: `index.md`

- [ ] **Step 1: Create the required files**

Use patch-based file creation for every new Markdown file listed above.

- [ ] **Step 2: Verify the files exist**

Run: `Get-ChildItem -Recurse`
Expected: the directories and files listed above are present

### Task 2: Write the core skill and support files

**Files:**
- Modify: `skills/project-curation/SKILL.md`
- Modify: `skills/project-curation/agents/openai.yaml`
- Modify: `skills/project-curation/templates/project-entry.md`
- Modify: `skills/project-curation/references/taxonomy.md`
- Modify: `skills/project-curation/adapters/opencode.md`
- Modify: `skills/project-curation/adapters/generic-agent.md`
- Modify: `index.md`

- [ ] **Step 1: Write the core workflow in `SKILL.md`**

Include trigger conditions, storage rules, classification rules, evidence rules, and index update rules.

- [ ] **Step 2: Add agent metadata**

Create a small `openai.yaml` with human-readable metadata that matches the skill purpose.

- [ ] **Step 3: Add reusable templates and references**

Create a project entry template and a taxonomy reference for consistent naming.

- [ ] **Step 4: Add OpenCode and generic agent adapters**

Describe how other agents should invoke the same workflow without changing the repository format.

- [ ] **Step 5: Seed the root bilingual index**

Add Chinese and English guidance plus starter sections for category and feature browsing.

### Task 3: Verify structure and consistency

**Files:**
- Verify: `docs/superpowers/specs/2026-06-06-project-curation-skill-design.md`
- Verify: `docs/superpowers/plans/2026-06-06-project-curation-skill.md`
- Verify: `skills/project-curation/SKILL.md`
- Verify: `skills/project-curation/agents/openai.yaml`
- Verify: `skills/project-curation/templates/project-entry.md`
- Verify: `skills/project-curation/references/taxonomy.md`
- Verify: `skills/project-curation/adapters/opencode.md`
- Verify: `skills/project-curation/adapters/generic-agent.md`
- Verify: `index.md`

- [ ] **Step 1: Check tree shape**

Run: `Get-ChildItem -Recurse`
Expected: all planned files appear under the expected directories

- [ ] **Step 2: Search for key conventions**

Run: `rg "category|feature|index.md|GitHub|local repository" skills docs index.md`
Expected: the workflow terms appear in the expected files

- [ ] **Step 3: Review for consistency**

Confirm that all files agree on:
- English-only directories and filenames
- Bilingual `index.md`
- Canonical storage path `categories/<category>/<feature>/<project-slug>.md`
