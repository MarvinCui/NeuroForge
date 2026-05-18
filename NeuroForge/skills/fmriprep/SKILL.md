---
name: fmriprep
description: Use this skill for fMRIPrep outputs, fMRI preprocessing reports, confounds, spaces, and BIDS derivatives interpretation.
domain: fMRI preprocessing
source: cleaned local skill corpus
---

# fMRIPrep Skill

## Purpose

This standalone skill helps Codex reason about fMRI preprocessing within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `fmriprep` skill folder independently.

## Use This Skill When

- A user provides fMRIPrep derivatives, reports, confounds, or preprocessed BOLD outputs.
- You need to plan fMRI preprocessing review, QC, confound selection, or downstream analysis.
- You need to connect BIDS inputs and fMRIPrep outputs to Nilearn or other fMRI analysis tools.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/other/index.rst`: Documentation reference for index.rst.
- `references/documentation/other/README.rst`: Documentation reference for README.rst.
- `references/documentation/overview/README.rst`: Documentation reference for README.rst.
- `references/documentation/overview/GOVERNANCE.md`: Documentation reference for GOVERNANCE.md.
- `references/documentation/overview/REFERENCES.md`: Documentation reference for REFERENCES.md.
- `references/documentation/overview/long_description.rst`: Documentation reference for long_description.rst.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/documentation/other/usage.rst`: Documentation reference for usage.rst.
- `references/documentation/other/outputs.rst`: Documentation reference for outputs.rst.
- `references/documentation/other/workflows.rst`: Documentation reference for workflows.rst.
- `references/tutorials/bidssourcefile/bidssourcefile.md`: Tutorial or worked example for bidssourcefile.md.
- `references/documentation/other/PIs.md`: Documentation reference for PIs.md.

## Common Workflows

- Inspect fMRIPrep derivative outputs and HTML reports
- Plan confound selection for Nilearn analysis
- Check output spaces and transform availability
- Route BOLD derivatives into GLM or connectivity workflows

## Search Terms

- `fMRIPrep`
- `BOLD`
- `confounds`
- `HTML report`
- `output spaces`
- `susceptibility distortion`
- `slice timing`
- `motion correction`
- `aCompCor`
- `framewise displacement`
- `carpet plot`
- `derivatives`

## Related Skills

- `bids-specification`
- `nilearn`
- `nibabel`
- `afni`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
