# Generic Agent Adapter

Use this adapter for agents that support plain prompt files, system instructions, or workspace conventions but do not support Codex-native skills.

## Required Inputs

- one GitHub repository URL or one local repository path
- access to this repository's `skills/project-curation/` folder

## Required Outputs

- one canonical note at `categories/<category>/<feature>/<project-slug>.md`
- an updated bilingual `index.md`

## Prompt Skeleton

```text
You are curating a saved software project into a personal repository.

Read the workflow rules in:
- skills/project-curation/SKILL.md
- skills/project-curation/templates/project-entry.md
- skills/project-curation/references/taxonomy.md

Then:
1. Inspect the provided repository URL or local path
2. Choose one primary category and one primary feature
3. Write or update the canonical note
4. Update the bilingual root index.md
5. Separate direct evidence from inference
```

## Consistency Rule

The repository contract is the source of truth. Any agent-specific convenience should preserve the same output paths, naming conventions, and note structure.
