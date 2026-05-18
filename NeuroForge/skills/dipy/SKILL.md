---
name: dipy
description: Use this skill for diffusion MRI reconstruction, registration, denoising, tracking, and validation workflows in Python.
domain: diffusion MRI reconstruction and tractography
source: cleaned local skill corpus
---

# DIPY Skill

## Purpose

This standalone skill helps Codex reason about diffusion MRI reconstruction and tractography within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `dipy` skill folder independently.

## Use This Skill When

- A user asks about diffusion MRI reconstruction and tractography in a psychology or neuroscience workflow.
- You need to route files, metadata, or analysis questions to DIPY-specific documentation.
- You need to draft safe plans, command suggestions, QC checks, or expected outputs without running heavy processing automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/examples/README.md`: Documentation reference for README.md.
- `references/documentation/other/README.md`: Documentation reference for README.md.
- `references/documentation/other/index.rst`: Documentation reference for index.rst.
- `references/documentation/guides/index.rst`: Documentation reference for index.rst.
- `references/documentation/other/README.rst`: Documentation reference for README.rst.
- `references/documentation/overview/README.rst`: Documentation reference for README.rst.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/tutorials/signal-index/signal-index.md`: Tutorial or worked example for signal-index.md.
- `references/tutorials/indexing-on-tensor-fit/indexing-on-tensor-fit.md`: Tutorial or worked example for indexing-on-tensor-fit.md.
- `references/tutorials/real-sh-descoteaux-from-index/real-sh-descoteaux-from-index.md`: Tutorial or worked example for real-sh-descoteaux-from-index.md.
- `references/documentation/guides/data.rst`: Documentation reference for data.rst.
- `references/documentation/other/data_fetch.rst`: Documentation reference for data_fetch.rst.

## Common Workflows

- Plan diffusion reconstruction or denoising
- Validate diffusion model outputs
- Inspect registration or tracking workflows
- Compare reconstruction assumptions against MRtrix3 outputs

## Search Terms

- `DIPY`
- `DWI`
- `reconstruction`
- `denoising`
- `registration`
- `tracking`
- `streamlines`
- `tensor`
- `response`
- `validation`
- `diffusion model`
- `tractography`

## Related Skills

- `qsiprep`
- `mrtrix3`
- `nibabel`
- `nilearn`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
