# freesurfer Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Faq

- Kind: `documentation`
- Source: `references/documentation/overview/FAQ.md`
- Note: Documentation code block extracted for implementation use.

```bash
recon-all -version
recon-all -s subjid -all > /dev/null 2>&1 \
recon-all -make all -s subject
recon-all -autorecon1 -noskullstrip -s \
recon-all -autrecon2 -autorecon3 -s \
recon-all -skullstrip -wsthresh 35 -clean-bm -no-wsgcaatlas -subjid
recon-all -skullstrip -no-wsgcaatlas -s \
recon-all -autorecon2 -autorecon3 -s \
mris_thickness -max \ to generate a thickness with a
mris_thickness -max 10 bert lh newlh.thickness**\
recon-all -make all -s subjid
recon-all -all -s bert -label-v1
```

## 2. FreeSurfer Coordinate Systems

- Kind: `documentation`
- Source: `references/documentation/overview/CoordinateSystems.md`
- Note: Documentation code block extracted for implementation use.

```bash
mri = MRIread('file.mgz'); % Can also read mgh, nii, nii.gz, img
VoxCRS = inv(Torig)\*\[tkrR tkrA tkrS 1\]'
movCRS = inv(Tmov)\*Reg\*\[tkrR tkrA tkrS 1\]'
origCRS = inv(Torig) \* Reg \* Tmov \* \[movC movR movS 1\]'
tkrRAS = inv(Reg) \* Tmov \* \[movC movR movS 1\]'
mri_vol2vol --reg $FREESURFER_HOME/average/mni152.register.dat --mov MNI152.nii.gz --targ orig.mgz --inv --o fsaverage.orig.mni152.mgz
mri_label2vol --reg $FREESURFER_HOME/average/mni152.register.dat --seg aparc+aseg.mgz --temp MNI152.nii.gz --o aparc+aseg.mni152.mgz
```

## 3. ReconAllTableStable7.1.1

- Kind: `documentation`
- Source: `references/documentation/overview/ReconAllTableStableV6.0.md`
- Note: Documentation code block extracted for implementation use.

```bash
recon-all -autorecon1 -subjid
mri_convert invol1.dcm orig/001.mgz
mri_convert invol2.dcm orig/002.mgz
mri_convert --no_scale 1 invol.dcm orig/T2raw.mgz
mri_robust_template --mov 001.mgz 002.mgz --average 1
mri_convert rawavg.mgz orig.mgz --conform
mri_add_xform_to_header -c transforms/talairach.xfm
mri_normalize -g 1 -mprage nu.mgz T1.mgz
mri_em_register -skull nu.mgz
mri_watershed -T1 -brain_atlas
recon-all -autorecon2 -subjid
mri_em_register -uns 3 -mask brainmask.mgz nu.mgz
```
