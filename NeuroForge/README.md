# Psychology / Neuroscience Codex Skill Collection

This repository is a standalone, GitHub-ready Codex Skill collection for psychology and neuroscience research workflows. It helps Codex inspect user-provided data, classify likely modalities, route to workflow templates, choose relevant tool-specific skills, and produce safe processing plans.

The collection covers BIDS, fMRI, DWI, EEG/MEG, behavioral experiments, Bayesian modeling, workflow reproducibility, registration, and neuroimaging file IO.

## How Codex Should Use It

1. Read `SKILL.md` for the collection-level entrypoint.
2. Inspect user-provided files or folders with `scripts/inspect_input.py`.
3. Route the detected input with `scripts/route_workflow.py` or `graph/skill_graph_summary.tsv`.
4. Read a relevant template in `workflows/`.
5. Read `skills/<tool>/SKILL.md` before going deeper into that skill's `references/`.
6. Generate a safe plan and ask before heavy processing unless the user explicitly requested execution.

## Using Individual Skills

You can use this repository in two ways.

The full repository is suitable for scenarios that require automatic routing, cross-tool planning, unified validation, cross-skill relationships, and example workflows.

A standalone `skills/<tool>/` folder is suitable when you only need one tool or one category of tasks. Each tool folder is written so that its `SKILL.md` can be understood independently.

When using a single skill independently, keep at least that folder's `SKILL.md` and any existing `references/` content. Do not create empty reference folders if a copied skill does not include one.

When a single skill mentions related skills or workflows, return to the complete collection to inspect the corresponding skill folder, workflow template, graph relationship, or example.

## Inspect And Plan From Inputs

Example commands:

```bash
python scripts/inspect_input.py examples/fake_bids
python scripts/build_plan.py examples/fake_bids --goal fmri-preprocessing
python scripts/inspect_input.py examples/fake_behavior/jspsych_results.csv
python scripts/build_plan.py examples/fake_behavior/jspsych_results.csv --goal behavioral-analysis
python scripts/inspect_input.py examples/fake_eeg/sub-01_task-test_eeg.vhdr
python scripts/build_plan.py examples/fake_eeg/sub-01_task-test_eeg.vhdr --goal eeg-preprocessing
```

## Repository Layout

```text
psych-neuro-codex-skill/
  README.md
  AGENTS.md
  SKILL.md
  MANIFEST.tsv
  .gitignore
  skills/
  workflows/
  graph/
  scripts/
  examples/
  reports/
```

## Safety Restrictions

The helper scripts are safe inspection and planning tools only. They must not execute fMRIPrep, QSIPrep, FreeSurfer, MRtrix3, AFNI, MNE preprocessing pipelines, PyMC sampling, Docker, Snakemake, or Nipype workflows. They may suggest commands as inert text.

Do not modify raw input data unless the user explicitly asks. Prefer workflow templates, documentation, tutorials, references, and tool-specific `SKILL.md` files over changelogs, tests, or generated metadata.

## Validation Commands

```bash
find . -type l -print
python scripts/inspect_input.py examples/fake_bids
python scripts/build_plan.py examples/fake_bids --goal fmri-preprocessing
python scripts/inspect_input.py examples/fake_behavior/jspsych_results.csv
python scripts/build_plan.py examples/fake_behavior/jspsych_results.csv --goal behavioral-analysis
python scripts/inspect_input.py examples/fake_eeg/sub-01_task-test_eeg.vhdr
python scripts/build_plan.py examples/fake_eeg/sub-01_task-test_eeg.vhdr --goal eeg-preprocessing
```
