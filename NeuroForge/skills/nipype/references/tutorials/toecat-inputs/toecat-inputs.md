# How To: Toecat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ToEcat inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), ignore_acquisition_variable=dict(argstr='-ignore_acquisition_variable'), ignore_ecat_acquisition_variable=dict(argstr='-ignore_ecat_acquisition_variable'), ignore_ecat_main=dict(argstr='-ignore_ecat_main'), ignore_ecat_subheader_variable=dict(argstr='-ignore_ecat_subheader_variable'), ignore_patient_variable=dict(argstr='-ignore_patient_variable'), ignore_study_variable=dict(argstr='-ignore_study_variable'), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), no_decay_corr_fctr=dict(argstr='-no_decay_corr_fctr'), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, keep_extension=False, name_source=['input_file'], name_template='%s_to_ecat.v', position=-1), voxels_as_integers=dict(argstr='-label'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), ignore_acquisition_variable=dict(argstr='-ignore_acquisition_variable'), ignore_ecat_acquisition_variable=dict(argstr='-ignore_ecat_acquisition_variable'), ignore_ecat_main=dict(argstr='-ignore_ecat_main'), ignore_ecat_subheader_variable=dict(argstr='-ignore_ecat_subheader_variable'), ignore_patient_variable=dict(argstr='-ignore_patient_variable'), ignore_study_variable=dict(argstr='-ignore_study_variable'), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), no_decay_corr_fctr=dict(argstr='-no_decay_corr_fctr'), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, keep_extension=False, name_source=['input_file'], name_template='%s_to_ecat.v', position=-1), voxels_as_integers=dict(argstr='-label'))
```

## Next Steps


---

*Source: test_auto_ToEcat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*