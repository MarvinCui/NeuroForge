# NeuroForge

NeuroForge is a curated collection of Codex-compatible Skills for psychology, cognitive science, and neuroscience research workflows. It brings together tool-specific guidance, reference material, routing metadata, and workflow templates so an AI coding assistant can reason more safely about research data, analysis plans, and reproducible pipelines.

The collection is designed for planning and documentation support first. It helps route a question to the right tool family, identify relevant references, draft safe processing plans, and surface common quality-control checks before any heavy analysis is run.

## What's Inside

The repository currently includes Skills for:

| Skill | Focus |
| --- | --- |
| `afni` | AFNI-oriented neuroimaging workflows, registration, command planning, and QC |
| `bids-specification` | BIDS datasets, metadata, derivatives, events, and layout validation |
| `dipy` | Diffusion MRI processing, registration, tractography, and Python workflows |
| `eeglab` | EEG analysis and EEGLAB-oriented preprocessing concepts |
| `fmriprep` | fMRI preprocessing outputs, confounds, reports, and derivative inspection |
| `freesurfer` | Anatomical segmentation, surface reconstruction, and `recon-all` outputs |
| `jspsych` | Browser-based behavioral experiments, timelines, plugins, and trial data |
| `mne-python` | EEG/MEG preprocessing, epoching, evoked responses, TFR, and source localization |
| `mrtrix3` | Diffusion MRI, tractography, connectomes, and MRtrix3 command planning |
| `nibabel` | Neuroimaging file IO, NIfTI handling, affine transforms, and image metadata |
| `nilearn` | fMRI GLM, connectivity, masking, confounds, and statistical maps |
| `nipype` | Workflow orchestration and neuroimaging pipeline interfaces |
| `psychopy` | Behavioral experiment design and PsychoPy workflow support |
| `pymc` | Bayesian modeling, probabilistic analysis, and statistical planning |
| `qsiprep` | Diffusion preprocessing, BIDS inputs, and QSIPrep derivative review |
| `snakemake` | Reproducible workflow management and pipeline organization |

It also includes cross-tool workflow templates for common research paths:

- `fmri_bids_fmriprep_nilearn`
- `dwi_qsiprep_mrtrix_dipy`
- `eeg_psychopy_mne`
- `web_experiment_jspsych_behavioral_stats`
- `multimodal_bids_pipeline`
- `reproducible_workflow_snakemake_docker`

## Repository Layout

```text
.
├── README.md
├── LICENSE
├── BuildFile/
│   └── output/              # Raw build-time Skills for developer tuning
└── NeuroForge/
    ├── AGENTS.md            # Agent-facing operating instructions
    ├── SKILL.md             # Collection-level Skill entrypoint
    ├── MANIFEST.tsv         # File inventory for the packaged collection
    ├── graph/               # Tool-concept routing graph and summary tables
    ├── skills/              # Final individual standalone Skill folders
    └── workflows/           # End-to-end workflow templates
```

`BuildFile/` contains the original Skills produced during construction. These files are useful for developers who want to inspect, debug, or tune the build process, but they are not the final Skills intended for normal use.

The finalized Skills are in `NeuroForge/skills/`.

## How To Use

Start with the collection entrypoint:

```text
NeuroForge/SKILL.md
```

For a tool-specific task, open the matching folder:

```text
NeuroForge/skills/<skill-name>/SKILL.md
```

Use `NeuroForge/skills/` as the source of truth for the final Skills. Use `BuildFile/output/` only when you need to inspect the raw build-time material or adjust the construction process.

Each folder under `NeuroForge/skills/` can also be used independently. To use only one Skill, copy that complete Skill folder into your Codex `skills` directory and keep its internal structure intact, including `SKILL.md`, `references/`, and any supporting files.

For cross-tool planning, use:

```text
NeuroForge/workflows/
NeuroForge/graph/skill_graph_summary.tsv
```

Each Skill is meant to be useful on its own, but the full collection is best when a question spans multiple parts of a research workflow, such as BIDS to fMRIPrep to Nilearn, PsychoPy to MNE-Python, or QSIPrep to MRtrix3 and DIPY.

## Safety And Scope

These Skills are not a substitute for official documentation, statistical review, clinical judgment, or domain supervision. They are intended to help an AI assistant inspect, route, plan, explain, and draft commands with care.

In particular:

- Do not modify raw research data unless the user explicitly asks.
- Do not run heavy tools such as fMRIPrep, QSIPrep, FreeSurfer, MRtrix3, AFNI, MNE pipelines, PyMC sampling, Docker, Snakemake, or Nipype workflows without explicit approval.
- Prefer official documentation and current project guidance when version-specific behavior matters.
- Treat generated metadata, examples, tests, and pattern-detection output as supporting context, not primary evidence.

## How This Repository Was Built

This project was assembled from Skills and reference material downloaded from official websites or GitHub repositories for the relevant tools and projects. The collection was then organized and adapted using the [Skill-Seekers](https://github.com/yusufkaraaslan/Skill_Seekers) Tool, Codex, and manual review/editing.

The goal of those adjustments was to make the material easier for Codex-style agents to route, read, and use responsibly in psychology and neuroscience research workflows.

## Acknowledgements

With sincere gratitude to all of the open-source projects, maintainers, researchers, documentation writers, and community contributors whose work made these Skills possible.

Special thanks to the creators and maintainers of the [Skill-Seekers](https://github.com/yusufkaraaslan/Skill_Seekers) Tool. [Skill-Seekers](https://github.com/yusufkaraaslan/Skill_Seekers) made it possible to gather and structure the source material into a form that could be further refined with Codex and careful manual adjustment.

## License

This repository is released under the MIT License. See `LICENSE` for details.

Please also respect the licenses and citation requirements of the upstream projects represented in the Skills and references.