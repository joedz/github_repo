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
Classify the project with one primary category and one primary feature.
Create or update the project note under categories/<category>/<feature>/<project-slug>.md.
Update the bilingual root index.md.
Mark inference clearly when evidence is incomplete.
```

## Compatibility Rule

Do not change the file layout, naming rules, or bilingual index format for OpenCode. Adapter files only change how the workflow is invoked.
