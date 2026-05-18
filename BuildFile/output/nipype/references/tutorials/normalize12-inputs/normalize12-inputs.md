# How To: Normalize12 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Normalize12 inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(affine_regularization_type=dict(field='eoptions.affreg'), apply_to_files=dict(copyfile=True, field='subj.resample'), bias_fwhm=dict(field='eoptions.biasfwhm'), bias_regularization=dict(field='eoptions.biasreg'), deformation_file=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='subj.def', mandatory=True, xor=['image_to_align', 'tpm']), image_to_align=dict(copyfile=True, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='subj.vol', mandatory=True, xor=['deformation_file']), jobtype=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='woptions.prefix', usedefault=True), paths=dict(), sampling_distance=dict(field='eoptions.samp'), smoothness=dict(field='eoptions.fwhm'), tpm=dict(copyfile=False, extensions=None, field='eoptions.tpm', xor=['deformation_file']), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), warping_regularization=dict(field='eoptions.reg'), write_bounding_box=dict(field='woptions.bb'), write_interp=dict(field='woptions.interp'), write_voxel_sizes=dict(field='woptions.vox'))
```


## Complete Example

```python
# Workflow
input_map = dict(affine_regularization_type=dict(field='eoptions.affreg'), apply_to_files=dict(copyfile=True, field='subj.resample'), bias_fwhm=dict(field='eoptions.biasfwhm'), bias_regularization=dict(field='eoptions.biasreg'), deformation_file=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='subj.def', mandatory=True, xor=['image_to_align', 'tpm']), image_to_align=dict(copyfile=True, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='subj.vol', mandatory=True, xor=['deformation_file']), jobtype=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='woptions.prefix', usedefault=True), paths=dict(), sampling_distance=dict(field='eoptions.samp'), smoothness=dict(field='eoptions.fwhm'), tpm=dict(copyfile=False, extensions=None, field='eoptions.tpm', xor=['deformation_file']), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), warping_regularization=dict(field='eoptions.reg'), write_bounding_box=dict(field='woptions.bb'), write_interp=dict(field='woptions.interp'), write_voxel_sizes=dict(field='woptions.vox'))
```

## Next Steps


---

*Source: test_auto_Normalize12.py:6 | Complexity: Beginner | Last updated: 2026-05-18*