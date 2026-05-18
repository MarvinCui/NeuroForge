---
name: mrtrix3
description: Use this skill for diffusion MRI tractography, FOD modeling, streamline filtering, and connectome generation.
domain: diffusion MRI tractography
source: cleaned local skill corpus
---

# MRtrix3 Skill

## Purpose

This standalone skill helps Codex reason about diffusion MRI tractography within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `mrtrix3` skill folder independently.

## Use This Skill When

- A user asks about diffusion MRI tractography in a psychology or neuroscience workflow.
- You need to route files, metadata, or analysis questions to MRtrix3-specific documentation.
- You need to draft safe plans, command suggestions, QC checks, or expected outputs without running heavy processing automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/examples/examples.md`: Documentation reference for examples.md.
- `references/documentation/api/connectome2tck.rst`: API reference for connectome2tck.rst.
- `references/documentation/api/connectomeedit.rst`: API reference for connectomeedit.rst.
- `references/documentation/api/tck2connectome.rst`: API reference for tck2connectome.rst.
- `references/documentation/api/connectomestats.rst`: API reference for connectomestats.rst.
- `references/documentation/examples/per_datum_processing.md`: Documentation reference for per_datum_processing.md.
- `references/documentation/examples/per_datum_multithreaded_processing.md`: Documentation reference for per_datum_multithreaded_processing.md.
- `references/documentation/examples/per_voxel_multithreaded_processing.md`: Documentation reference for per_voxel_multithreaded_processing.md.
- `references/documentation/api/mrcat.rst`: API reference for mrcat.rst.
- `references/documentation/api/5ttgen.rst`: API reference for 5ttgen.rst.
- `references/documentation/api/amp2sh.rst`: API reference for amp2sh.rst.
- `references/documentation/api/dirgen.rst`: API reference for dirgen.rst.

## Common Workflows

- Plan FOD estimation and tractography
- Plan ACT and streamline filtering steps
- Generate connectome workflow outlines
- Check DWI-to-atlas space assumptions

## Search Terms

- `MRtrix3`
- `tckgen`
- `tcksift`
- `tcksift2`
- `dwi2fod`
- `5ttgen`
- `FOD`
- `ACT`
- `tractography`
- `connectome`
- `streamlines`
- `response function`

## Related Skills

- `qsiprep`
- `dipy`
- `nibabel`
- `bids-specification`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
