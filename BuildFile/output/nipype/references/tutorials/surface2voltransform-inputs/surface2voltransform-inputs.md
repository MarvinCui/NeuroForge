# How To: Surface2Voltransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Surface2VolTransform inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), hemi=dict(argstr='--hemi %s', mandatory=True), mkmask=dict(argstr='--mkmask', xor=['source_file']), projfrac=dict(argstr='--projfrac %s'), reg_file=dict(argstr='--volreg %s', extensions=None, mandatory=True, xor=['subject_id']), source_file=dict(argstr='--surfval %s', copyfile=False, extensions=None, mandatory=True, xor=['mkmask']), subject_id=dict(argstr='--identity %s', xor=['reg_file']), subjects_dir=dict(argstr='--sd %s'), surf_name=dict(argstr='--surf %s'), template_file=dict(argstr='--template %s', extensions=None), transformed_file=dict(argstr='--outvol %s', extensions=None, hash_files=False, name_source=['source_file'], name_template='%s_asVol.nii'), vertexvol_file=dict(argstr='--vtxvol %s', extensions=None, hash_files=False, name_source=['source_file'], name_template='%s_asVol_vertex.nii'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), hemi=dict(argstr='--hemi %s', mandatory=True), mkmask=dict(argstr='--mkmask', xor=['source_file']), projfrac=dict(argstr='--projfrac %s'), reg_file=dict(argstr='--volreg %s', extensions=None, mandatory=True, xor=['subject_id']), source_file=dict(argstr='--surfval %s', copyfile=False, extensions=None, mandatory=True, xor=['mkmask']), subject_id=dict(argstr='--identity %s', xor=['reg_file']), subjects_dir=dict(argstr='--sd %s'), surf_name=dict(argstr='--surf %s'), template_file=dict(argstr='--template %s', extensions=None), transformed_file=dict(argstr='--outvol %s', extensions=None, hash_files=False, name_source=['source_file'], name_template='%s_asVol.nii'), vertexvol_file=dict(argstr='--vtxvol %s', extensions=None, hash_files=False, name_source=['source_file'], name_template='%s_asVol_vertex.nii'))
```

## Next Steps


---

*Source: test_auto_Surface2VolTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*