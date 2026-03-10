# Contributing to ChemClaw

This repository is a test/example skills pack for chemistry workflows.

Anyone can install skills from this repo with:

```bash
npx skills add little1d/ChemClaw
```

## Skill Folder Conventions

Put each skill in its own folder with a required `SKILL.md`:

- `skills/.curated/<skill-name>/SKILL.md`: stable, recommended skills
- `skills/.experimental/<skill-name>/SKILL.md`: drafts or unstable skills

## Add a New Skill

1. Define the scope
   - Write the target task in one sentence.
   - Write 3-5 user prompts that should trigger the skill.
   - Decide expected outputs (for example: table, checklist, JSON, SMILES).
2. Choose a folder
   - stable: `skills/.curated`
   - draft: `skills/.experimental`
3. Create a new directory

```bash
mkdir -p skills/.curated/<skill-name>
```

1. Create `SKILL.md` with frontmatter

```md
---
name: your-skill-name
description: What this skill does and when it should trigger.
---

# Your Skill Title

Write clear, actionable instructions for the agent.
```

1. Fill the body using this recommended outline
   - Goal and output contract
   - Required inputs and accepted formats
   - Core workflow (numbered steps)
   - Validation and sanity checks
   - Error handling and uncertainty reporting
   - Output templates/examples
2. Keep names lowercase with hyphens (example: `acid-base-titration-helper`).
3. Test discovery locally

```bash
npx skills add . --list
```

1. Test single-skill install locally

```bash
npx skills add . --skill your-skill-name
```

1. If relevant, test on at least two real prompts
   - one straightforward case
   - one ambiguous or noisy case

## Content Quality Checklist

- `name` and `description` exist and are plain strings.
- `description` includes both capability and trigger context.
- Instructions are specific enough to run, not just conceptual notes.
- No fabricated scientific claims; uncertainty is stated clearly.
- Output format is explicit and parseable when needed.
- The skill states assumptions and missing inputs.

## Pull Request Checklist

- Added/updated `SKILL.md`
- Verified `npx skills add . --list` works
- Verified `npx skills add . --skill <name>` works
- Included at least one realistic usage example in the PR description
