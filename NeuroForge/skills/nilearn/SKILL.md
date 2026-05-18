---
name: nilearn
description: Use this skill for fMRI statistical modeling, connectomes, masking, image operations, and machine learning workflows in Python.
domain: fMRI analysis, GLM, connectomes, machine learning
source: cleaned local skill corpus
---

# Nilearn Skill

## Purpose

This standalone skill helps Codex reason about fMRI analysis, GLM, connectomes, machine learning within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `nilearn` skill folder independently.

## Use This Skill When

- A user asks about fMRI analysis, GLM, connectomes, machine learning in a psychology or neuroscience workflow.
- You need to route files, metadata, or analysis questions to Nilearn-specific documentation.
- You need to draft safe plans, command suggestions, QC checks, or expected outputs without running heavy processing automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/examples/README.rst`: Documentation reference for README.rst.
- `references/documentation/examples/report_note.rst`: Documentation reference for report_note.rst.
- `references/documentation/examples/html_repr_note.rst`: Documentation reference for html_repr_note.rst.
- `references/documentation/other/README.md`: Documentation reference for README.md.
- `references/documentation/other/index.rst`: Documentation reference for index.rst.
- `references/documentation/overview/AGENTS.md`: Documentation reference for AGENTS.md.
- `references/documentation/overview/CLAUDE.md`: Documentation reference for CLAUDE.md.
- `references/documentation/overview/README.rst`: Documentation reference for README.rst.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/tutorials/select-from-index/select-from-index.md`: Tutorial or worked example for select-from-index.md.
- `references/documentation/other/glm.rst`: Documentation reference for glm.rst.
- `references/documentation/other/datasets.rst`: Documentation reference for datasets.rst.

## Common Workflows

- Plan first-level and second-level GLM analysis
- Build masker and connectome workflows
- Inspect image compatibility before modeling
- Route fMRIPrep derivatives into statistical analysis

## Search Terms

- `FirstLevelModel`
- `SecondLevelModel`
- `design matrix`
- `contrast`
- `GLM`
- `masker`
- `ConnectivityMeasure`
- `atlas`
- `parcellation`
- `NIfTI`
- `connectome`
- `machine learning`
- `stat map`

## Related Skills

- `fmriprep`
- `bids-specification`
- `nibabel`
- `pymc`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
