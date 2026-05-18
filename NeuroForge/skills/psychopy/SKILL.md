---
name: psychopy
description: Use this skill for PsychoPy experiment design, Builder concepts, trial handling, stimuli, responses, and task logging.
domain: behavioral experiment design
source: cleaned local skill corpus
---

# PsychoPy Skill

## Purpose

This standalone skill helps Codex reason about behavioral experiment design within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `psychopy` skill folder independently.

## Use This Skill When

- A user provides PsychoPy experiments, Builder files, trial conditions, or task logs.
- You need to plan stimulus, response, trigger, or event logging workflows.
- You need to connect lab task outputs to EEG, fMRI, or behavioral statistics.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/other/readme.md`: Documentation reference for readme.md.
- `references/documentation/features/readme.md`: Documentation reference for readme.md.
- `references/documentation/overview/README.md`: Documentation reference for README.md.
- `references/documentation/architecture/README.md`: Documentation reference for README.md.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/documentation/other/2023.1.0.md`: Documentation reference for 2023.1.0.md.
- `references/documentation/other/2024.1.0.md`: Documentation reference for 2024.1.0.md.
- `references/documentation/authors/AUTHORS.md`: Documentation reference for AUTHORS.md.
- `references/documentation/community/code-of-conduct.md`: Documentation reference for code-of-conduct.md.
- `references/tutorials/get-data/get-data.md`: Tutorial or worked example for get-data.md.
- `references/tutorials/random-data-skills/random-data-output.md`: Tutorial or worked example for random-data-output.md.
- `references/tutorials/json-dump-with-data/json-dump-with-data.md`: Tutorial or worked example for json-dump-with-data.md.

## Common Workflows

- Plan lab experiment structure and trial logging
- Map stimuli, responses, and triggers
- Prepare event logs for EEG or fMRI
- Review behavioral output columns

## Search Terms

- `PsychoPy`
- `Builder`
- `TrialHandler`
- `routine`
- `stimulus`
- `keyboard`
- `response`
- `trigger`
- `eyetracking`
- `experiment`
- `conditions`
- `logging`

## Related Skills

- `jspsych`
- `mne-python`
- `pymc`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
