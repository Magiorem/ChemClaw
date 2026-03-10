# NMR Elucidation Example

This file shows one compact example input and output shape for the `nmr-structure-elucidator` skill.

## Example Input

```text
1H NMR (400 MHz, CDCl3):
7.26 (m, 5H)
3.65 (s, 2H)

13C NMR (100 MHz, CDCl3):
137.8, 128.6, 128.3, 126.9, 40.8

Molecular formula: C7H8
```

## Example Output (Expected Format)

```text
Input summary
- 1H NMR: 7.26 (m, 5H), 3.65 (s, 2H)
- 13C NMR: 137.8, 128.6, 128.3, 126.9, 40.8
- Formula / constraints: C7H8

Derived constraints
- Unsaturation index: 4
- Key motif clues: monosubstituted aromatic-like proton cluster near 7.2 ppm; benzylic CH2-like signal near 3.6 ppm

Candidate structures (ranked)
1) SMILES: Cc1ccccc1
   Score: 0.73
   Why it fits: aromatic region + benzylic environment pattern
   Conflicts or weak points: integration/chemical-shift simplification in this toy example

Peak assignment table
- 7.26 ppm (m, 5H) -> aromatic ring protons
- 3.65 ppm (s, 2H) -> benzylic methylene-like environment
- 137.8/128.6/128.3/126.9 ppm -> aromatic carbons
- 40.8 ppm -> aliphatic carbon near aromatic system

Confidence
- Overall: medium
- Main uncertainty: this example is intentionally simplified and omits coupling detail
- What extra data would disambiguate: COSY/HSQC/HMBC and better-resolved integrations
```

## Notes

- Values above are for demonstration of structure and format, not a validated benchmark dataset.
- For real tasks, provide full peak metadata and acquisition conditions whenever possible.
