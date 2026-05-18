# Multimodal BIDS Pipeline

## Scope
Workflow assistance for studies combining behavioral data, fMRI, DWI, EEG/MEG, and derivative-level cross-modal analysis under one BIDS-centered structure.

## Input Requirements
- BIDS root with consistent participant, session, task, acquisition, and run labels.
- Behavioral trial data linked to neuroimaging or EEG/MEG events.
- Modality-specific raw files and metadata for fMRI, DWI, EEG/MEG, and anatomical imaging.
- Analysis plan describing cross-modal variables, shared covariates, and output spaces.

## Main Steps
1. Audit participant/session/run identifiers across modalities.
2. Validate behavioral events and trial metadata against task files.
3. Route fMRI through fMRIPrep and task/connectivity analysis.
4. Route DWI through QSIPrep, tractography, reconstruction, or connectome analysis.
5. Route EEG/MEG through preprocessing, epoching, evoked/TFR, or source analysis.
6. Harmonize derivative outputs by subject, session, space, atlas, and condition.
7. Build cross-modal tables or models that preserve provenance from each modality.

## Relevant Tools
- `bids-specification`
- `fmriprep`
- `qsiprep`
- `mrtrix3`
- `dipy`
- `mne-python`
- `nilearn`
- `pymc`
- `snakemake`

## Common Failure Points
- Participant IDs differ across behavioral and neuroimaging files.
- Events are defined differently across fMRI and EEG tasks.
- Derivatives mix spaces or atlases without clear labels.
- Cross-modal models use different exclusion criteria by modality.
- Metadata is copied forward without checking acquisition differences.

## Quality Checks
- BIDS validation and manual metadata audit.
- Per-modality QC reports reviewed before cross-modal analysis.
- Event counts and condition labels reconciled across modalities.
- Derivative tables include source filenames and preprocessing versions.
- Cross-modal model inputs have explicit missing-data and exclusion rules.

## Expected Outputs
- Clean BIDS root and modality-specific derivatives.
- Cross-modal subject/session/run manifest.
- Analysis-ready tables with behavioral, fMRI, DWI, and EEG/MEG measures.
- QC summary covering metadata consistency and derivative provenance.

## Search Terms For This Corpus
`BIDS`, `events.tsv`, `behavioral data`, `fmriprep`, `QSIPrep`, `MRtrix`, `DIPY`, `MNE`, `derivatives`, `confounds`, `connectome`, `reproducibility`
