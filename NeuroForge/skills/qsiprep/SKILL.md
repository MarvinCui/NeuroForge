---
name: qsiprep
description: Use this skill for diffusion MRI preprocessing, QSIPrep outputs, DWI metadata, and diffusion quality control planning.
domain: diffusion MRI preprocessing
source: cleaned local skill corpus
---

# QSIPrep Skill

## Purpose

This standalone skill helps Codex reason about diffusion MRI preprocessing within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `qsiprep` skill folder independently.

## Use This Skill When

- A user provides DWI data, QSIPrep outputs, gradient files, or diffusion preprocessing reports.
- You need to plan DWI QC, correction review, or routing to tractography/reconstruction.
- You need to inspect whether BIDS DWI metadata is sufficient for preprocessing.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/other/index.rst`: Documentation reference for index.rst.
- `references/documentation/overview/AGENTS.md`: Documentation reference for AGENTS.md.
- `references/documentation/overview/README.rst`: Documentation reference for README.rst.
- `references/documentation/overview/long_description.rst`: Documentation reference for long_description.rst.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/documentation/other/usage.rst`: Documentation reference for usage.rst.
- `references/documentation/other/preprocessing.rst`: Documentation reference for preprocessing.rst.
- `references/documentation/other/api.rst`: Documentation reference for api.rst.
- `references/documentation/other/base.rst`: Documentation reference for base.rst.
- `references/documentation/other/help.rst`: Documentation reference for help.rst.
- `references/documentation/other/links.rst`: Documentation reference for links.rst.
- `references/documentation/other/license.rst`: Documentation reference for license.rst.

## Common Workflows

- Inspect DWI metadata and QSIPrep derivative outputs
- Plan diffusion preprocessing quality checks
- Route preprocessed DWI to MRtrix3 or DIPY
- Document gradient, fieldmap, and correction assumptions

## Search Terms

- `QSIPrep`
- `DWI`
- `bvec`
- `bval`
- `eddy`
- `topup`
- `susceptibility correction`
- `gradient`
- `fieldmap`
- `preprocessed diffusion`
- `QC`
- `derivatives`

## Related Skills

- `bids-specification`
- `mrtrix3`
- `dipy`
- `nibabel`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
