---
name: afni
description: Use this skill for AFNI-oriented MRI and fMRI command-line workflow planning, QC, and dataset inspection.
domain: fMRI / MRI command-line neuroimaging
source: cleaned local skill corpus
---

# AFNI Skill

## Purpose

This standalone skill helps Codex reason about fMRI / MRI command-line neuroimaging within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `afni` skill folder independently.

## Use This Skill When

- A user asks about fMRI / MRI command-line neuroimaging in a psychology or neuroscience workflow.
- You need to route files, metadata, or analysis questions to AFNI-specific documentation.
- You need to draft safe plans, command suggestions, QC checks, or expected outputs without running heavy processing automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/other/README.md`: Documentation reference for README.md.
- `references/documentation/other/index.rst`: Documentation reference for index.rst.
- `references/documentation/other/README.rst`: Documentation reference for README.rst.
- `references/documentation/overview/README.rst`: Documentation reference for README.rst.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/documentation/other/cover.rst`: Documentation reference for cover.rst.
- `references/documentation/other/ROI_45a.rst`: Documentation reference for ROI_45a.rst.
- `references/documentation/other/glossary.rst`: Documentation reference for glossary.rst.
- `references/documentation/other/roistoc1.rst`: Documentation reference for roistoc1.rst.
- `references/documentation/other/macaquetoc1.rst`: Documentation reference for macaquetoc1.rst.
- `references/documentation/other/Demonstrations.md`: Documentation reference for Demonstrations.md.
- `references/documentation/other/connectionstoc1.rst`: Documentation reference for connectionstoc1.rst.

## Common Workflows

- Plan AFNI command-line MRI or fMRI steps
- Inspect motion, masks, and registration assumptions
- Review AFNI-style QC checkpoints
- Route command outputs to downstream analysis

## Search Terms

- `AFNI`
- `3dTstat`
- `3dvolreg`
- `3dDeconvolve`
- `afni_proc.py`
- `NIfTI`
- `BOLD`
- `QC`
- `registration`
- `motion`
- `mask`
- `dataset`

## Related Skills

- `fmriprep`
- `nilearn`
- `nibabel`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
