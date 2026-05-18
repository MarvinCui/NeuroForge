---
name: NeuroForge
description: Use this skill when the user provides psychology, neuroscience, neuroimaging, EEG, MEG, behavioral, BIDS, NIfTI, DICOM, fMRI, DWI, or experiment data and asks Codex to inspect, route, plan, process, validate, or analyze it.
---

# NeuroForge Workflow Skill

## Purpose

This repository is a standalone Codex skill package for psychology and neuroscience workflows. It helps Codex inspect user-provided files or folders, classify the input type, route to the right workflow, route to the right tool-specific skill, generate safe processing plans, suggest commands, and avoid unsafe automatic execution unless the user explicitly asks for it.

The package can be used as a complete routed collection, or a single `skills/<tool>/` folder can be copied and used independently for one tool or task family.

## How Codex Should Use This Repository

1. Read this top-level `SKILL.md`.
2. If the user provides a file or folder, run `scripts/inspect_input.py`.
3. Check `skills/<tool>/SKILL.md` for tool-specific guidance.
4. Check `skills/<tool>/references` only when more detail is needed.
5. Generate a plan.
6. Ask before running heavy processing commands unless the user explicitly requested execution.

## Supported Input Types

- BIDS dataset folders
- NIfTI files
- DICOM folders
- EEG and MEG files
- PsychoPy experiments
- jsPsych data
- Behavioral CSV / TSV / JSON files
- Statistical tables
- Workflow directories

## Routing Rules

BIDS structure:
- `skills/bids-specification`

fMRIPrep outputs or fMRI preprocessing:
- `skills/fmriprep`
- `skills/bids-specification`
- `skills/nilearn`
- `skills/nibabel`

Diffusion MRI:
- `skills/qsiprep`
- `skills/mrtrix3`
- `skills/dipy`
- `skills/nibabel`
- `skills/bids-specification`

EEG / MEG:
- `skills/mne-python`
- `skills/eeglab`
- `skills/bids-specification`

Behavioral experiments:
- `skills/psychopy`
- `skills/jspsych`

Bayesian modeling and statistics:
- `skills/pymc`

Workflow and reproducibility:
- `skills/snakemake`
- `skills/nipype`

Registration:
- `skills/afni`
- `skills/freesurfer`

Image IO:
- `skills/nibabel`

## Safety Rules

- Do not modify raw input data unless the user explicitly asks.
- Do not run fMRIPrep, QSIPrep, FreeSurfer, MRtrix3, AFNI, MNE processing pipelines, or PyMC sampling without explicit user approval.
- Do not treat changelogs as primary evidence.
- Do not prioritize test examples.
- Do not use local absolute paths as knowledge.
- Do not treat generated design-pattern detection as reliable architecture truth.
- Prefer workflows, documentation, tutorials, references, and tool-specific `SKILL.md` files.
