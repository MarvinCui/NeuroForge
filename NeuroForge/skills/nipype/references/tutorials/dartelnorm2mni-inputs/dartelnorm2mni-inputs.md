# How To: Dartelnorm2Mni Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DARTELNorm2MNI inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(apply_to_files=dict(copyfile=False, field='mni_norm.data.subjs.images', mandatory=True), bounding_box=dict(field='mni_norm.bb'), flowfield_files=dict(field='mni_norm.data.subjs.flowfields', mandatory=True), fwhm=dict(field='mni_norm.fwhm'), matlab_cmd=dict(), mfile=dict(usedefault=True), modulate=dict(field='mni_norm.preserve'), paths=dict(), template_file=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='mni_norm.template', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), voxel_size=dict(field='mni_norm.vox'))
```


## Complete Example

```python
# Workflow
input_map = dict(apply_to_files=dict(copyfile=False, field='mni_norm.data.subjs.images', mandatory=True), bounding_box=dict(field='mni_norm.bb'), flowfield_files=dict(field='mni_norm.data.subjs.flowfields', mandatory=True), fwhm=dict(field='mni_norm.fwhm'), matlab_cmd=dict(), mfile=dict(usedefault=True), modulate=dict(field='mni_norm.preserve'), paths=dict(), template_file=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='mni_norm.template', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), voxel_size=dict(field='mni_norm.vox'))
```

## Next Steps


---

*Source: test_auto_DARTELNorm2MNI.py:6 | Complexity: Beginner | Last updated: 2026-05-18*