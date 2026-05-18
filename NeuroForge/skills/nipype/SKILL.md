---
name: nipype
description: Use this skill for neuroimaging workflow orchestration and interfaces that connect multiple processing tools.
domain: workflow orchestration and neuroimaging interfaces
source: cleaned local skill corpus
---

# Nipype Skill

## Purpose

This standalone skill helps Codex reason about workflow orchestration and neuroimaging interfaces within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `nipype` skill folder independently.

## Use This Skill When

- A user asks about workflow orchestration and neuroimaging interfaces in a psychology or neuroscience workflow.
- You need to route files, metadata, or analysis questions to Nipype-specific documentation.
- You need to draft safe plans, command suggestions, QC checks, or expected outputs without running heavy processing automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/examples/README.md`: Documentation reference for README.md.
- `references/documentation/other/index.rst`: Documentation reference for index.rst.
- `references/documentation/overview/README.rst`: Documentation reference for README.rst.
- `references/documentation/overview/THANKS.rst`: Documentation reference for THANKS.rst.
- `references/tutorials/index.md`: Tutorial or worked example for index.md.
- `references/tutorials/qualityindex-inputs/qualityindex-inputs.md`: Tutorial or worked example for qualityindex-inputs.md.
- `references/tutorials/similarityindex-inputs/similarityindex-inputs.md`: Tutorial or worked example for similarityindex-inputs.md.
- `references/tutorials/extractnrrdvectorindex-inputs/extractnrrdvectorindex-inputs.md`: Tutorial or worked example for extractnrrdvectorindex-inputs.md.
- `references/documentation/other/git_resources.rst`: Documentation reference for git_resources.rst.
- `references/documentation/workflows/workflow_failure.md`: Documentation reference for workflow_failure.md.
- `references/documentation/other/development_workflow.rst`: Documentation reference for development_workflow.rst.
- `references/tutorials/glm-outputs/glm-outputs.md`: Tutorial or worked example for glm-outputs.md.

## Common Workflows

- Plan multi-tool neuroimaging interfaces
- Sketch workflow nodes and data flow
- Connect AFNI or FreeSurfer steps
- Review execution graph assumptions

## Search Terms

- `Nipype`
- `workflow`
- `node`
- `interface`
- `pipeline`
- `MapNode`
- `DataSink`
- `AFNI interface`
- `execution graph`

## Related Skills

- `snakemake`
- `afni`
- `freesurfer`

## Cautions

- Do not execute workflows automatically; ask before running interface graphs.
- Check external tool availability and output directories before execution.
- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
