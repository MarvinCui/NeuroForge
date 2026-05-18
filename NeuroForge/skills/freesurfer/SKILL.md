---
name: freesurfer
description: Use this skill for FreeSurfer surface reconstruction, anatomical segmentation, recon-all outputs, and cortical surface workflows.
domain: surface reconstruction and anatomical processing
source: cleaned local skill corpus
---

# FreeSurfer Skill

## Purpose

This standalone skill helps Codex reason about surface reconstruction and anatomical processing within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `freesurfer` skill folder independently.

## Use This Skill When

- A user asks about surface reconstruction and anatomical processing in a psychology or neuroscience workflow.
- You need to route files, metadata, or analysis questions to FreeSurfer-specific documentation.
- You need to draft safe plans, command suggestions, QC checks, or expected outputs without running heavy processing automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/overview/FreeSurferCommandsRegistration.md`: Documentation reference for FreeSurferCommandsRegistration.md.
- `references/documentation/overview/FAQ.md`: Documentation reference for FAQ.md.
- `references/documentation/overview/index.md`: Documentation reference for index.md.
- `references/documentation/overview/Glossary.md`: Documentation reference for Glossary.md.
- `references/documentation/overview/Tutorials.md`: Documentation reference for Tutorials.md.
- `references/documentation/overview/FileFormats.md`: Documentation reference for FileFormats.md.
- `references/documentation/overview/QuickInstall.md`: Documentation reference for QuickInstall.md.
- `references/documentation/overview/ReconAllTable.md`: Documentation reference for ReconAllTable.md.
- `references/documentation/overview/FreeSurferWiki.md`: Documentation reference for FreeSurferWiki.md.
- `references/documentation/overview/CoordinateSystems.md`: Documentation reference for CoordinateSystems.md.
- `references/documentation/overview/FreeSurferSupport.md`: Documentation reference for FreeSurferSupport.md.
- `references/documentation/overview/DownloadAndInstall.md`: Documentation reference for DownloadAndInstall.md.

## Common Workflows

- Plan anatomical reconstruction review
- Inspect surface and segmentation outputs
- Route surfaces to MNE or Nilearn workflows
- Check subject directory and fsaverage assumptions

## Search Terms

- `FreeSurfer`
- `recon-all`
- `surface`
- `aparc`
- `aseg`
- `fsaverage`
- `cortical thickness`
- `segmentation`
- `mri_convert`
- `subject directory`

## Related Skills

- `mne-python`
- `fmriprep`
- `nilearn`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
