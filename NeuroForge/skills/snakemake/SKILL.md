---
name: snakemake
description: Use this skill for reproducible workflow design, rules, DAGs, logging, provenance, and container-aware pipelines.
domain: workflow management and reproducibility
source: cleaned local skill corpus
---

# Snakemake Skill

## Purpose

This standalone skill helps Codex reason about workflow management and reproducibility within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `snakemake` skill folder independently.

## Use This Skill When

- A user needs a reproducible workflow around BIDS inputs and derivatives.
- You need to plan rules, DAGs, configs, logs, containers, or provenance.
- You need to suggest workflow commands without launching jobs automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/api/index.rst`: API reference for index.rst.
- `references/documentation/api/snakemake.report.html_reporter.data.rst`: API reference for snakemake.report.html_reporter.data.rst.
- `references/documentation/api/modules.rst`: API reference for modules.rst.
- `references/documentation/api/snakemake.rst`: API reference for snakemake.rst.
- `references/documentation/api/snakemake_api.rst`: API reference for snakemake_api.rst.
- `references/documentation/api/module_template.rst`: API reference for module_template.rst.
- `references/documentation/api/snakemake_utils.rst`: API reference for snakemake_utils.rst.
- `references/documentation/api/snakemake.assets.rst`: API reference for snakemake.assets.rst.
- `references/documentation/api/snakemake.common.rst`: API reference for snakemake.common.rst.
- `references/documentation/api/snakemake.remote.rst`: API reference for snakemake.remote.rst.
- `references/documentation/api/snakemake.report.rst`: API reference for snakemake.report.rst.
- `references/documentation/api/snakemake.script.rst`: API reference for snakemake.script.rst.

## Common Workflows

- Plan reproducible workflow rules
- Define inputs, outputs, logs, and config
- Route BIDS derivatives through a pipeline
- Capture provenance and validation artifacts

## Search Terms

- `Snakemake`
- `Snakefile`
- `rule`
- `workflow`
- `DAG`
- `input`
- `output`
- `params`
- `threads`
- `log`
- `provenance`
- `container`
- `config`

## Related Skills

- `bids-specification`
- `fmriprep`
- `qsiprep`
- `nipype`

## Cautions

- Do not launch workflows automatically; ask before running jobs.
- Check declared inputs, outputs, logs, configs, and environments before execution.
- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.
