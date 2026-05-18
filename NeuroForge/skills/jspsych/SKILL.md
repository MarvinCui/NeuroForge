---
name: jspsych
description: Use this skill for browser-based behavioral experiments, jsPsych timelines, plugins, trial data, and reaction-time tasks.
domain: browser-based behavioral experiments
source: cleaned local skill corpus
---

# jsPsych Skill

## Purpose

This standalone skill helps Codex reason about browser-based behavioral experiments within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `jspsych` skill folder independently.

## Use This Skill When

- A user provides browser experiment code or jsPsych trial data.
- You need to plan timeline, plugin, reaction time, accuracy, or data export review.
- You need to route behavioral tables into statistics or Bayesian modeling.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/examples/README-template.md`: Documentation reference for README-template.md.
- `references/documentation/api/jspsych-data.md`: API reference for jspsych-data.md.
- `references/documentation/api/jspsych.md`: API reference for jspsych.md.
- `references/documentation/api/jspsych-turk.md`: API reference for jspsych-turk.md.
- `references/documentation/api/jspsych-utils.md`: API reference for jspsych-utils.md.
- `references/documentation/api/jspsych-pluginAPI.md`: API reference for jspsych-pluginAPI.md.
- `references/documentation/api/jspsych-randomization.md`: API reference for jspsych-randomization.md.
- `references/documentation/other/index.md`: Documentation reference for index.md.
- `references/documentation/other/README.md`: Documentation reference for README.md.
- `references/documentation/overview/README.md`: Documentation reference for README.md.
- `references/documentation/architecture/README.md`: Documentation reference for README.md.
- `references/documentation/overview/contributors.md`: Documentation reference for contributors.md.

## Common Workflows

- Plan browser experiment timelines
- Review plugin and trial metadata choices
- Inspect reaction-time and accuracy data
- Route exported data to statistics workflows

## Search Terms

- `jsPsych`
- `timeline`
- `plugin`
- `jsPsych.run`
- `browser`
- `html-keyboard-response`
- `trial_type`
- `rt`
- `response`
- `stimulus`
- `accuracy`
- `data export`

## Related Skills

- `psychopy`
- `pymc`
- `snakemake`

## Cautions

- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
