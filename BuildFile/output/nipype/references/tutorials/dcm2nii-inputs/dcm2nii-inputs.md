# How To: Dcm2Nii Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Dcm2nii inputs

## Prerequisites

**Required Modules:**
- `dcm2nii`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(anonymize=dict(argstr='-a', usedefault=True), args=dict(argstr='%s'), collapse_folders=dict(argstr='-c', usedefault=True), config_file=dict(argstr='-b %s', extensions=None, genfile=True), convert_all_pars=dict(argstr='-v', usedefault=True), date_in_filename=dict(argstr='-d', usedefault=True), environ=dict(nohash=True, usedefault=True), events_in_filename=dict(argstr='-e', usedefault=True), gzip_output=dict(argstr='-g', usedefault=True), id_in_filename=dict(argstr='-i', usedefault=True), nii_output=dict(argstr='-n', usedefault=True), output_dir=dict(argstr='-o %s', genfile=True), protocol_in_filename=dict(argstr='-p', usedefault=True), reorient=dict(argstr='-r'), reorient_and_crop=dict(argstr='-x', usedefault=True), source_dir=dict(argstr='%s', mandatory=True, position=-1, xor=['source_names']), source_in_filename=dict(argstr='-f', usedefault=True), source_names=dict(argstr='%s', copyfile=False, mandatory=True, position=-1, xor=['source_dir']), spm_analyze=dict(argstr='-s', xor=['nii_output']))
```


## Complete Example

```python
# Workflow
input_map = dict(anonymize=dict(argstr='-a', usedefault=True), args=dict(argstr='%s'), collapse_folders=dict(argstr='-c', usedefault=True), config_file=dict(argstr='-b %s', extensions=None, genfile=True), convert_all_pars=dict(argstr='-v', usedefault=True), date_in_filename=dict(argstr='-d', usedefault=True), environ=dict(nohash=True, usedefault=True), events_in_filename=dict(argstr='-e', usedefault=True), gzip_output=dict(argstr='-g', usedefault=True), id_in_filename=dict(argstr='-i', usedefault=True), nii_output=dict(argstr='-n', usedefault=True), output_dir=dict(argstr='-o %s', genfile=True), protocol_in_filename=dict(argstr='-p', usedefault=True), reorient=dict(argstr='-r'), reorient_and_crop=dict(argstr='-x', usedefault=True), source_dir=dict(argstr='%s', mandatory=True, position=-1, xor=['source_names']), source_in_filename=dict(argstr='-f', usedefault=True), source_names=dict(argstr='%s', copyfile=False, mandatory=True, position=-1, xor=['source_dir']), spm_analyze=dict(argstr='-s', xor=['nii_output']))
```

## Next Steps


---

*Source: test_auto_Dcm2nii.py:6 | Complexity: Beginner | Last updated: 2026-05-18*