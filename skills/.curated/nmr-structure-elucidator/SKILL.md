---
name: nmr-structure-elucidator
description: Elucidate molecular structures from 1H NMR and 13C NMR data, including peak lists or spectrum images, and return candidate structures as SMILES plus interpretable assignment tables. Use when users ask to solve unknown compounds from HNMR/CNMR, compare candidate structures, or convert spectral clues into structural hypotheses.
---

# NMR Structure Elucidator

Produce candidate molecular structures from NMR evidence and report confidence transparently.

Accepted inputs:

1. 1H NMR peak list (delta, multiplicity, integration, J when available)
2. 13C NMR peak list (delta, optional DEPT tags)
3. Optional molecular formula or exact mass
4. Optional image(s) of spectra

Examples:

- See `examples/basic-nmr-elucidation.md` for a compact input/output pattern.

## Workflow

1. Parse inputs into normalized tables
   - Keep units and solvent/frequency metadata.
   - Flag missing metadata explicitly.
2. Compute constraints
   - Estimate unsaturation index if formula is available.
   - Count unique proton/carbon environments.
   - Identify diagnostic regions (aromatic, aldehyde, carbonyl-adjacent, etc.).
3. Build fragment hypotheses
   - Use integration + multiplicity + coupling to infer local proton neighborhoods.
   - Use 13C shifts to propose functional group fragments.
4. Assemble candidate structures
   - Generate 1-5 plausible candidates.
   - Ensure each candidate satisfies formula and unsaturation when provided.
5. Score and rank candidates
   - Score by consistency with observed peaks and splitting patterns.
   - Penalize unresolved or contradictory assignments.
6. Return structure outputs
   - Provide canonical SMILES for each candidate.
   - Provide an assignment table mapping observed peaks to atoms/fragments.
   - If asked for graph output, provide atom-bond adjacency text.
7. Handle spectrum images
   - First transcribe approximate peak positions/intensities from images.
   - Mark image-derived values as approximate.
   - Ask for confirmation when low-resolution images create ambiguity.
8. Optional structure image generation
   - If runtime tools are available, generate 2D structure depictions for top candidates.
   - If tools are unavailable, return SMILES and a clear note that rendering was skipped.

## Output Contract

Use this format:

```text
Input summary
- 1H NMR:
- 13C NMR:
- Formula / constraints:

Derived constraints
- Unsaturation index:
- Key motif clues:

Candidate structures (ranked)
1) SMILES: ...
   Score: ...
   Why it fits: ...
   Conflicts or weak points: ...

Peak assignment table
- Peak -> proposed atom/fragment mapping

Confidence
- Overall: high | medium | low
- Main uncertainty:
- What extra data would disambiguate:
```

## Rules

1. Do not present uncertain assignments as confirmed facts.
2. When multiple structures fit, provide ranked alternatives.
3. If input is insufficient, ask for missing peaks, formula, or 2D NMR (COSY/HSQC/HMBC).
