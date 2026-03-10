# ChemClaw

ChemClaw is a public skills package for chemistry-focused AI workflows.

## Install

```bash
npx skills add little1d/ChemClaw
```

Install only one skill:

```bash
npx skills add little1d/ChemClaw --skill nmr-structure-elucidator
```

List skills from this package:

```bash
npx skills add little1d/ChemClaw --list
```

## Repository Layout

- `skills/.curated/`: stable skills for general usage
- `skills/.experimental/`: work-in-progress skills

Each skill directory contains a `SKILL.md` file with:

- `name`: skill identifier
- `description`: what the skill does and when to trigger it

## Example Skills

- `nmr-structure-elucidator`: infer candidate structures from 1H/13C NMR lists or images, then return ranked SMILES and assignments
- `stoichiometry-solver`: solve mole/mass/concentration and limiting-reagent tasks

## Contributing

See `CONTRIBUTING.md` for how to add a new skill, file structure, and review checklist.
