# OpenCode Adapter

Use this adapter when the agent runtime is OpenCode or another environment that does not natively load Codex `SKILL.md` files.

## Invocation Pattern

Tell the agent to follow the `project-curation` repository workflow and point it at:

- `skills/project-curation/SKILL.md`
- `skills/project-curation/templates/project-entry.md`
- `skills/project-curation/references/taxonomy.md`

## Minimum Prompt

```text
Use the project-curation workflow in this repository.
Input: <GitHub URL or local repository path>
Mode: <entry-curation or explicit reclassification>
Classify the project by core workflow. If it belongs in ai-tools, choose its primary AI role.
Create, update, or explicitly reclassify the canonical note under categories/<category>/<feature-or-role>/<project-slug>.md.
If reclassifying, move the note when needed, remove stale duplicates, and update the bilingual root index.md.
Mark inference clearly when evidence is incomplete.
```

## Compatibility Rule

Do not change the file layout, naming rules, or bilingual index format for OpenCode. Adapter files only change how the workflow is invoked.
