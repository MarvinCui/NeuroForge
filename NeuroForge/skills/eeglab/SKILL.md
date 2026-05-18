---
name: eeglab
description: Use this skill for EEGLAB-oriented EEG preprocessing, ICA, event handling, and MATLAB-based EEG analysis planning.
domain: EEG preprocessing and analysis
source: cleaned local skill corpus
---

# EEGLAB Skill

## Purpose

This standalone skill helps Codex reason about EEG preprocessing and analysis within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `eeglab` skill folder independently.

## Use This Skill When

- A user asks about EEG preprocessing and analysis in a psychology or neuroscience workflow.
- You need to route files, metadata, or analysis questions to EEGLAB-specific documentation.
- You need to draft safe plans, command suggestions, QC checks, or expected outputs without running heavy processing automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/overview/AGENTS.md`: Documentation reference for AGENTS.md.
- `references/documentation/overview/CLAUDE.md`: Documentation reference for CLAUDE.md.
- `references/documentation/overview/README.md`: Documentation reference for README.md.
- `references/documentation/other/SKILL.md`: Documentation reference for SKILL.md.
- `references/documentation/templates/bug_report.md`: Documentation reference for bug_report.md.
- `references/documentation/community/CODE_OF_CONDUCT.md`: Documentation reference for CODE_OF_CONDUCT.md.
- `references/documentation/templates/new-plugin-or-plugin-update.md`: Documentation reference for new-plugin-or-plugin-update.md.

## Common Workflows

- Plan EEG import and preprocessing in EEGLAB
- Review ICA and artifact handling
- Map events to epochs and ERP workflows
- Compare MATLAB EEG steps with MNE or FieldTrip

## Search Terms

- `EEGLAB`
- `EEG`
- `ICA`
- `artifact`
- `events`
- `epochs`
- `filter`
- `rereference`
- `channel locations`
- `ERP`
- `time-frequency`

## Related Skills

- `mne-python`
- `psychopy`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
