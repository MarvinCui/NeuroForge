---
name: mne-python
description: Use this skill for EEG and MEG preprocessing, epoching, evoked responses, time-frequency analysis, and source localization in Python.
domain: EEG / MEG analysis in Python
source: cleaned local skill corpus
---

# MNE-Python Skill

## Purpose

This standalone skill helps Codex reason about EEG / MEG analysis in Python within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `mne-python` skill folder independently.

## Use This Skill When

- A user provides EEG or MEG recordings, event files, epochs, evoked data, or source-analysis questions.
- You need to plan filtering, ICA, epoching, time-frequency analysis, or source localization in Python.
- You need to connect experiment logs to electrophysiology events.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/api/events.rst`: API reference for events.rst.
- `references/documentation/api/datasets.rst`: API reference for datasets.rst.
- `references/documentation/api/source_space.rst`: API reference for source_space.rst.
- `references/documentation/api/preprocessing.rst`: API reference for preprocessing.rst.
- `references/documentation/api/reading_raw_data.rst`: API reference for reading_raw_data.rst.
- `references/documentation/api/mri.rst`: API reference for mri.rst.
- `references/documentation/api/export.rst`: API reference for export.rst.
- `references/documentation/api/report.rst`: API reference for report.rst.
- `references/documentation/api/file_io.rst`: API reference for file_io.rst.
- `references/documentation/api/forward.rst`: API reference for forward.rst.
- `references/documentation/api/inverse.rst`: API reference for inverse.rst.
- `references/documentation/api/logging.rst`: API reference for logging.rst.

## Common Workflows

- Plan EEG or MEG preprocessing
- Map events into epochs and conditions
- Plan ICA, evoked, TFR, and source workflows
- Check exported measures for statistics

## Search Terms

- `MNE`
- `raw`
- `filter`
- `notch`
- `ICA`
- `bad channels`
- `events`
- `epochs`
- `event_id`
- `evoked`
- `TFR`
- `morlet`
- `source estimate`
- `BEM`
- `forward solution`
- `inverse operator`

## Related Skills

- `bids-specification`
- `eeglab`
- `psychopy`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
