# fMRI BIDS to fMRIPrep to Nilearn Workflow

## Scope
End-to-end task fMRI workflow assistance from BIDS raw data through fMRIPrep preprocessing and Nilearn GLM or connectivity analysis.

## Input Requirements
- BIDS-valid raw dataset with `dataset_description.json`, `participants.tsv`, `sub-*/ses-*`, functional BOLD files, events files, and fieldmap metadata when available.
- fMRIPrep derivatives with preprocessed BOLD images, brain masks, confounds TSV files, transforms, and HTML reports.
- Analysis plan describing task design, contrasts, groups, or connectivity targets.

## Main Steps
1. Validate the BIDS layout and confirm `events.tsv` columns: `onset`, `duration`, `trial_type`, and task-specific behavioral fields.
2. Run or inspect fMRIPrep preprocessing outputs, including output spaces, susceptibility distortion correction, motion correction, and normalization.
3. Select confounds for nuisance regression, such as motion parameters, framewise displacement, aCompCor, and non-steady-state indicators.
4. Build Nilearn first-level models with `FirstLevelModel`, design matrices, contrasts, and subject-level maps.
5. Build second-level models with `SecondLevelModel` or run connectivity analysis with masker objects and correlation matrices.
6. Store outputs under BIDS derivatives with clear `desc-`, `space-`, and `stat-` labels.

## Relevant Tools
- `bids-specification`
- `fmriprep`
- `nilearn`
- `nibabel`
- `snakemake`

## Common Failure Points
- Missing or inconsistent `events.tsv` timing.
- Confounds file not aligned with the selected preprocessed BOLD run.
- Incorrect output space for the intended atlas or group analysis.
- High motion without motion-outlier handling.
- Mixing raw BIDS paths and derivatives paths in analysis code.

## Quality Checks
- BIDS validation passes or known warnings are documented.
- fMRIPrep HTML reports reviewed for registration, masks, fieldmaps, and carpet plots.
- Design matrix columns match the experimental design.
- Confound regressors are inspected for missing or all-zero columns.
- Group model inputs use consistent spaces, smoothing, and contrast definitions.

## Expected Outputs
- Preprocessed BOLD derivatives and fMRIPrep reports.
- First-level design matrices, contrast maps, and statistical maps.
- Second-level maps or connectivity matrices.
- QC notes tied to subject, session, and run identifiers.

## Search Terms For This Corpus
`BIDS`, `fmriprep`, `bold`, `confounds`, `FirstLevelModel`, `SecondLevelModel`, `design matrix`, `contrast`, `ConnectivityMeasure`, `quality control`, `derivatives`
