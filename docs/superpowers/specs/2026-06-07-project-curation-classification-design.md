# Project Curation Classification Design

**Date:** 2026-06-07

## Goal

Refine the `project-curation` skill so it can classify newly added repositories more accurately in an AI-heavy collection, avoid turning `ai-tools` into a catch-all bucket, and keep README indexes limited to categories that actually exist in the repository.

## Problem Statement

The current taxonomy works for a small collection, but it has two structural issues:

1. `ai-tools` is too broad and keeps absorbing projects that differ in purpose, architecture, and workflow role.
2. The index rendering pattern is based on a preset category list, so README files show empty sections for categories that have no stored projects.

This makes the collection harder to scan and weakens the value of the skill as the repository grows.

## Design Principles

- Choose the primary `category` by the repository's core workflow contribution, not by surface form such as CLI, website, plugin, or SDK.
- Use `ai-tools` only when the repository's main value is serving an AI, agent, model, memory, prompt, evaluation, or context workflow.
- When a repository belongs in `ai-tools`, require an additional reasoning step: identify the repository's primary role inside an AI system.
- Prefer stable, reusable labels over one-off project-specific names.
- Allow creation of a new classification label when existing labels do not fit, but only if the new label describes a durable responsibility that can plausibly group future projects.
- Render README indexes from the projects that are actually present on disk, not from a fixed list of all possible categories.

## Repository Contract Changes

The existing storage contract remains mostly intact:

- Public entries stay under `<project-root>/categories/<category>/<feature-or-role>/<project-slug>.md`
- Local-only entries stay under `<project-root>/local_categories/<category>/<feature-or-role>/<project-slug>.md`
- Public indexes stay in `<project-root>/README.md`
- Local-only indexes stay in `<project-root>/README_LOCAL.md`

The main semantic change is that for `ai-tools`, the second path segment should represent the repository's primary AI system role instead of a generic standout feature whenever that gives a clearer classification.

For non-`ai-tools` categories, the existing feature-oriented interpretation can remain in place.

## Classification Flow

The skill should classify in two stages.

### Stage 1: Choose the Primary Category

The model must answer this question first:

> Which core development workflow does this repository primarily serve?

Examples:

- If the repository mainly improves agent orchestration, memory, context engineering, prompt operations, or model evaluation, it should usually be categorized as `ai-tools`.
- If AI is only a supporting capability but the main workflow is frontend implementation, CLI automation, infrastructure, or backend services, it should be categorized by that non-AI workflow instead.

This rule prevents repositories from being pulled into `ai-tools` just because they mention LLMs or ship an AI-facing feature.

### Stage 2: If Category Is `ai-tools`, Choose the Primary AI Role

If Stage 1 yields `ai-tools`, the model must answer a second question before choosing the path:

> What is this repository mainly responsible for inside an AI system?

This reasoning step should happen explicitly in the skill instructions. The model should determine the dominant role first, then map it to a stable slug.

Suggested reusable roles include:

- `agent-runtime`
- `agent-orchestration`
- `context-engineering`
- `memory`
- `evaluation`
- `prompt-ops`
- `tool-integration`
- `knowledge-ingestion`
- `knowledge-retrieval`
- `developer-experience`
- `interface`

These are examples, not a closed list.

## Rules for Creating a New AI Role

The skill should create a new AI role label only when all of the following are true:

1. No existing role expresses the repository's main responsibility without distortion.
2. The proposed label describes a system responsibility, not an implementation detail, framework choice, or marketing phrase.
3. The label is broad enough to plausibly group future repositories.
4. The label is not a near-duplicate of an existing role.

Examples of labels to avoid:

- technology-specific names such as `langchain-tools`
- vague value judgments such as `awesome-ai`
- narrow one-off phrases such as `meeting-summary-agent`

If a new role is created, it should be added to the taxonomy reference with a short explanation so later classifications stay consistent.

## Category vs Secondary Traits

The skill should distinguish between:

- primary classification: what workflow or AI role the repository mainly serves
- secondary traits: important but non-primary strengths such as strong UX, extensibility, testing quality, or visual design

Those secondary traits should be recorded in `secondary_features` or tags rather than forcing the primary path to represent every dimension of the project.

This keeps the directory structure stable while still preserving useful nuance.

## Taxonomy Changes

The taxonomy reference should be updated to reflect two separate ideas:

1. top-level categories by core workflow
2. AI-specific role labels used when `category = ai-tools`

The taxonomy should clearly say:

- category selection is based on core workflow
- `ai-tools` requires an extra AI-role decision
- existing labels should be reused first
- new labels are allowed only under the new-role rules above

For non-AI categories, the current feature suggestions can remain available.

## README Rendering Changes

README generation should switch from preset-section rendering to data-driven rendering.

The README should:

- show only categories that currently have at least one stored note
- omit empty categories instead of rendering placeholder rows
- derive category sections from actual files under `categories/` or `local_categories/`
- keep the compact stats block at the top

This change applies to both `README.md` and `README_LOCAL.md`.

## Skill Instruction Changes

The `project-curation` skill should be updated so that classification is an explicit reasoning task rather than a simple lookup task.

The instructions should require the model to:

1. infer the repository's core workflow from evidence
2. decide whether `ai-tools` is truly the primary category
3. if so, identify the repository's primary AI system role
4. reuse an existing role when possible
5. create a new role when necessary under the reuse rules
6. store non-primary strengths as secondary traits
7. render README sections only for categories that exist in the saved collection

## Affected Files

The likely implementation surface is:

- `skills/project-curation/SKILL.md`
- `skills/project-curation/references/taxonomy.md`
- `skills/project-curation/templates/project-entry.md`
- README generation logic or README authoring instructions in the skill

If the repository later adds scripts for note generation or README rebuilding, the same classification rules should be encoded there as well.

## Testing Strategy

Validation should focus on representative classification cases.

At minimum, test these scenarios:

1. A repository that looks like a CLI but mainly serves agent or context workflows should still classify as `ai-tools`.
2. A repository that mentions AI but is mainly a frontend or backend product should not be forced into `ai-tools`.
3. Two different AI repositories with clearly different responsibilities should land in different AI role paths.
4. A repository that does not fit any current AI role should trigger creation of one reusable new role.
5. README output should include only categories present on disk.
6. Local-only repositories should never appear in the public README.

## Risks and Mitigations

### Risk: The model still overuses `ai-tools`

Mitigation:
Make the Stage 1 question explicit and require evidence-backed reasoning about the repository's primary workflow.

### Risk: New AI roles proliferate too quickly

Mitigation:
Require new-role creation to satisfy the four reuse rules and update the taxonomy reference when a new role is introduced.

### Risk: Old entries become semantically inconsistent

Mitigation:
Treat future edits to existing notes as opportunities to migrate older `ai-tools` entries into clearer AI role paths when justified.

### Risk: README organization becomes unstable

Mitigation:
Keep the top-level category list stable and only make the rendered sections data-driven.

## Out of Scope

- Full automation scripts for repository ingestion
- Backfilling every existing project note immediately
- Multi-dimensional faceted navigation beyond the current README and note structure

## Recommended Implementation Order

1. Update the taxonomy reference to introduce the core-workflow rule and AI-role layer
2. Update `SKILL.md` so the classification reasoning is explicit
3. Update note-template guidance if needed to reflect role-based storage under `ai-tools`
4. Update README rendering instructions so only existing categories are shown
5. Reclassify existing `ai-tools` notes only where the current paths are clearly misleading
