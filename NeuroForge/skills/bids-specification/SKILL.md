---
name: bids-specification
description: Use this skill for BIDS dataset structure, metadata, naming, events, participants tables, and derivatives conventions.
domain: data standard and metadata
source: cleaned local skill corpus
---

# BIDS Specification Skill

## Purpose

This standalone skill helps Codex reason about data standard and metadata within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `bids-specification` skill folder independently.

## Use This Skill When

- A user asks about BIDS dataset layout, filenames, entities, sidecars, events, participants, or derivatives.
- You need to validate whether a workflow has enough metadata for fMRI, DWI, EEG, MEG, or behavioral analysis.
- You need to translate between raw data organization and downstream tool expectations.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/other/index.md`: Documentation reference for index.md.
- `references/documentation/other/README.md`: Documentation reference for README.md.
- `references/documentation/other/index.rst`: Documentation reference for index.rst.
- `references/documentation/overview/README.md`: Documentation reference for README.md.
- `references/documentation/overview/macros_doc.md`: Documentation reference for macros_doc.md.
- `references/documentation/overview/DECISION-MAKING.md`: Documentation reference for DECISION-MAKING.md.
- `references/documentation/overview/Maintainers_Guide.md`: Documentation reference for Maintainers_Guide.md.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/documentation/other/events.md`: Documentation reference for events.md.
- `references/documentation/other/common-data-types.md`: Documentation reference for common-data-types.md.
- `references/documentation/other/data-summary-files.md`: Documentation reference for data-summary-files.md.
- `references/documentation/other/dataset-description.md`: Documentation reference for dataset-description.md.

## Common Workflows

- Audit a raw dataset for BIDS naming and metadata completeness
- Map modality folders to downstream workflow requirements
- Plan derivatives naming and provenance metadata
- Check event, participant, and sidecar consistency

## Search Terms

- `BIDS`
- `dataset_description`
- `participants.tsv`
- `events.tsv`
- `sub-`
- `ses-`
- `anat`
- `func`
- `dwi`
- `eeg`
- `meg`
- `beh`
- `fmap`
- `derivatives`
- `metadata`
- `sidecar`
- `task`
- `run`
- `space`
- `desc`

## Related Skills

- `fmriprep`
- `qsiprep`
- `mne-python`
- `nilearn`
- `snakemake`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
