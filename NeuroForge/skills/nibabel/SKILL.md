---
name: nibabel
description: Use this skill for NIfTI, GIFTI, CIFTI, tractogram, and neuroimaging file input/output questions.
domain: neuroimaging file IO
source: cleaned local skill corpus
---

# NiBabel Skill

## Purpose

This standalone skill helps Codex reason about neuroimaging file IO within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `nibabel` skill folder independently.

## Use This Skill When

- A user asks about neuroimaging file IO in a psychology or neuroscience workflow.
- You need to route files, metadata, or analysis questions to NiBabel-specific documentation.
- You need to draft safe plans, command suggestions, QC checks, or expected outputs without running heavy processing automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/other/index.rst`: Documentation reference for index.rst.
- `references/documentation/other/README.rst`: Documentation reference for README.rst.
- `references/documentation/overview/README.rst`: Documentation reference for README.rst.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/documentation/other/nifti_images.rst`: Documentation reference for nifti_images.rst.
- `references/documentation/other/git_resources.rst`: Documentation reference for git_resources.rst.
- `references/documentation/other/data_pkg_discuss.rst`: Documentation reference for data_pkg_discuss.rst.
- `references/documentation/other/dicom_niftiheader.rst`: Documentation reference for dicom_niftiheader.rst.
- `references/documentation/other/maintainer_workflow.rst`: Documentation reference for maintainer_workflow.rst.
- `references/documentation/workflows/workflow_failure.md`: Documentation reference for workflow_failure.md.
- `references/documentation/other/development_workflow.rst`: Documentation reference for development_workflow.rst.
- `references/documentation/other/api.rst`: Documentation reference for api.rst.

## Common Workflows

- Inspect neuroimaging file headers and shapes
- Plan safe NIfTI/GIFTI/CIFTI loading
- Check affine and orientation metadata
- Support file conversion and metadata review

## Search Terms

- `NiBabel`
- `NIfTI`
- `GIFTI`
- `CIFTI`
- `MGH`
- `tractogram`
- `nib.load`
- `affine`
- `header`
- `image shape`
- `voxel`
- `orientation`
- `metadata`

## Related Skills

- `nilearn`
- `fmriprep`
- `qsiprep`
- `mrtrix3`
- `dipy`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
