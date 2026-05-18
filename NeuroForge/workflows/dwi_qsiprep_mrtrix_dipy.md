# DWI BIDS to QSIPrep to MRtrix3 and DIPY Workflow

## Scope
Diffusion MRI workflow assistance from BIDS DWI inputs through QSIPrep preprocessing, MRtrix3 tractography, DIPY reconstruction or validation, and connectome outputs.

## Input Requirements
- BIDS DWI dataset with DWI NIfTI files, `bval`, `bvec`, JSON sidecars, phase-encoding metadata, and reverse phase-encoded images when available.
- Anatomical T1w image for registration and tissue segmentation when tractography requires anatomical constraints.
- Atlas or parcellation for connectome construction.

## Main Steps
1. Confirm BIDS DWI metadata, gradient files, phase encoding, and intended fieldmap relationships.
2. Use QSIPrep outputs for denoising, eddy/topup or susceptibility correction, motion correction, and gradient handling.
3. Inspect QSIPrep QC reports and verify orientation, distortion correction, and registration.
4. Use MRtrix3 for response estimation, FOD generation with `dwi2fod`, anatomical priors with `5ttgen`, tractography with `tckgen`, and filtering with `tcksift` or `tcksift2`.
5. Use DIPY for reconstruction checks, model comparison, or independent validation of diffusion measures.
6. Generate connectome matrices from tractograms and parcellations, then document weights, streamline filters, and atlas space.

## Relevant Tools
- `bids-specification`
- `qsiprep`
- `mrtrix3`
- `dipy`
- `nibabel`

## Common Failure Points
- Reversed or corrupted `bvec` orientation.
- Missing phase-encoding metadata for susceptibility correction.
- Atlas and tractography outputs in different spaces.
- Tractography run without clear seeding, cutoff, or filtering parameters.
- Connectome matrices generated without parcellation provenance.

## Quality Checks
- Validate BIDS DWI naming and sidecars.
- Review QSIPrep visual reports and motion/distortion metrics.
- Check FOD images, tissue segmentation, and tractogram plausibility.
- Compare summary diffusion metrics or reconstructions in DIPY when needed.
- Confirm connectome matrix labels match atlas labels.

## Expected Outputs
- QSIPrep preprocessed DWI derivatives and reports.
- FOD images, tractograms, filtered tractograms, and connectome matrices.
- DIPY validation outputs or reconstruction summaries.
- Provenance notes for correction, tractography, and atlas choices.

## Search Terms For This Corpus
`QSIPrep`, `DWI`, `eddy`, `topup`, `bvec`, `bval`, `dwi2fod`, `5ttgen`, `tckgen`, `tcksift2`, `connectome`, `parcellation`
