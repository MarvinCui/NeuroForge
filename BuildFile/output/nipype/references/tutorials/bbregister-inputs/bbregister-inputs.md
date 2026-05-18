# How To: Bbregister Inputs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test BBRegister inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map_5_3 = dict(...)

```python
input_map_5_3 = dict(args=dict(argstr='%s'), contrast_type=dict(argstr='--%s', mandatory=True), dof=dict(argstr='--%d'), environ=dict(nohash=True, usedefault=True), epi_mask=dict(argstr='--epi-mask'), fsldof=dict(argstr='--fsl-dof %d'), init=dict(argstr='--init-%s', mandatory=True, xor=['init_reg_file']), init_cost_file=dict(argstr='--initcost %s'), init_reg_file=dict(argstr='--init-reg %s', mandatory=True, xor=['init']), intermediate_file=dict(argstr='--int %s'), out_fsl_file=dict(argstr='--fslmat %s'), out_lta_file=dict(argstr='--lta %s', min_ver='5.2.0'), out_reg_file=dict(argstr='--reg %s', genfile=True), reg_frame=dict(argstr='--frame %d', xor=['reg_middle_frame']), reg_middle_frame=dict(argstr='--mid-frame', xor=['reg_frame']), registered_file=dict(argstr='--o %s'), source_file=dict(argstr='--mov %s', copyfile=False, mandatory=True), spm_nifti=dict(argstr='--spm-nii'), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict())
```

**Verification:**
```python
assert getattr(instance.inputs.traits()[key], metakey) == value
```

### Step 2: Assign input_map_6_0 = dict(...)

```python
input_map_6_0 = dict(args=dict(argstr='%s'), contrast_type=dict(argstr='--%s', mandatory=True), dof=dict(argstr='--%d'), environ=dict(nohash=True, usedefault=True), epi_mask=dict(argstr='--epi-mask'), fsldof=dict(argstr='--fsl-dof %d'), init=dict(argstr='--init-%s', xor=['init_reg_file']), init_reg_file=dict(argstr='--init-reg %s', xor=['init']), init_cost_file=dict(argstr='--initcost %s'), intermediate_file=dict(argstr='--int %s'), out_fsl_file=dict(argstr='--fslmat %s'), out_lta_file=dict(argstr='--lta %s', min_ver='5.2.0'), out_reg_file=dict(argstr='--reg %s', genfile=True), reg_frame=dict(argstr='--frame %d', xor=['reg_middle_frame']), reg_middle_frame=dict(argstr='--mid-frame', xor=['reg_frame']), registered_file=dict(argstr='--o %s'), source_file=dict(argstr='--mov %s', copyfile=False, mandatory=True), spm_nifti=dict(argstr='--spm-nii'), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict())
```

### Step 3: Assign instance = BBRegister(...)

```python
instance = BBRegister()
```

### Step 4: Assign input_map = input_map_6_0

```python
input_map = input_map_6_0
```

### Step 5: Assign input_map = input_map_5_3

```python
input_map = input_map_5_3
```

**Verification:**
```python
assert getattr(instance.inputs.traits()[key], metakey) == value
```


## Complete Example

```python
# Workflow
input_map_5_3 = dict(args=dict(argstr='%s'), contrast_type=dict(argstr='--%s', mandatory=True), dof=dict(argstr='--%d'), environ=dict(nohash=True, usedefault=True), epi_mask=dict(argstr='--epi-mask'), fsldof=dict(argstr='--fsl-dof %d'), init=dict(argstr='--init-%s', mandatory=True, xor=['init_reg_file']), init_cost_file=dict(argstr='--initcost %s'), init_reg_file=dict(argstr='--init-reg %s', mandatory=True, xor=['init']), intermediate_file=dict(argstr='--int %s'), out_fsl_file=dict(argstr='--fslmat %s'), out_lta_file=dict(argstr='--lta %s', min_ver='5.2.0'), out_reg_file=dict(argstr='--reg %s', genfile=True), reg_frame=dict(argstr='--frame %d', xor=['reg_middle_frame']), reg_middle_frame=dict(argstr='--mid-frame', xor=['reg_frame']), registered_file=dict(argstr='--o %s'), source_file=dict(argstr='--mov %s', copyfile=False, mandatory=True), spm_nifti=dict(argstr='--spm-nii'), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict())
input_map_6_0 = dict(args=dict(argstr='%s'), contrast_type=dict(argstr='--%s', mandatory=True), dof=dict(argstr='--%d'), environ=dict(nohash=True, usedefault=True), epi_mask=dict(argstr='--epi-mask'), fsldof=dict(argstr='--fsl-dof %d'), init=dict(argstr='--init-%s', xor=['init_reg_file']), init_reg_file=dict(argstr='--init-reg %s', xor=['init']), init_cost_file=dict(argstr='--initcost %s'), intermediate_file=dict(argstr='--int %s'), out_fsl_file=dict(argstr='--fslmat %s'), out_lta_file=dict(argstr='--lta %s', min_ver='5.2.0'), out_reg_file=dict(argstr='--reg %s', genfile=True), reg_frame=dict(argstr='--frame %d', xor=['reg_middle_frame']), reg_middle_frame=dict(argstr='--mid-frame', xor=['reg_frame']), registered_file=dict(argstr='--o %s'), source_file=dict(argstr='--mov %s', copyfile=False, mandatory=True), spm_nifti=dict(argstr='--spm-nii'), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict())
instance = BBRegister()
if isinstance(instance.inputs, BBRegisterInputSpec6):
    input_map = input_map_6_0
else:
    input_map = input_map_5_3
for key, metadata in list(input_map.items()):
    for metakey, value in list(metadata.items()):
        assert getattr(instance.inputs.traits()[key], metakey) == value
```

## Next Steps


---

*Source: test_BBRegister.py:4 | Complexity: Intermediate | Last updated: 2026-05-18*