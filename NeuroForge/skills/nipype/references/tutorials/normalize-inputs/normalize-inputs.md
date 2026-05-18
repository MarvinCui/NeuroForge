# How To: Normalize Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Normalize inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(DCT_period_cutoff=dict(field='eoptions.cutoff'), affine_regularization_type=dict(field='eoptions.regtype'), apply_to_files=dict(copyfile=True, field='subj.resample'), jobtype=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), nonlinear_iterations=dict(field='eoptions.nits'), nonlinear_regularization=dict(field='eoptions.reg'), out_prefix=dict(field='roptions.prefix', usedefault=True), parameter_file=dict(copyfile=False, extensions=None, field='subj.matname', mandatory=True, xor=['source', 'template']), paths=dict(), source=dict(copyfile=True, field='subj.source', mandatory=True, xor=['parameter_file']), source_image_smoothing=dict(field='eoptions.smosrc'), source_weight=dict(copyfile=False, extensions=None, field='subj.wtsrc'), template=dict(copyfile=False, extensions=None, field='eoptions.template', mandatory=True, xor=['parameter_file']), template_image_smoothing=dict(field='eoptions.smoref'), template_weight=dict(copyfile=False, extensions=None, field='eoptions.weight'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), write_bounding_box=dict(field='roptions.bb'), write_interp=dict(field='roptions.interp'), write_preserve=dict(field='roptions.preserve'), write_voxel_sizes=dict(field='roptions.vox'), write_wrap=dict(field='roptions.wrap'))
```


## Complete Example

```python
# Workflow
input_map = dict(DCT_period_cutoff=dict(field='eoptions.cutoff'), affine_regularization_type=dict(field='eoptions.regtype'), apply_to_files=dict(copyfile=True, field='subj.resample'), jobtype=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), nonlinear_iterations=dict(field='eoptions.nits'), nonlinear_regularization=dict(field='eoptions.reg'), out_prefix=dict(field='roptions.prefix', usedefault=True), parameter_file=dict(copyfile=False, extensions=None, field='subj.matname', mandatory=True, xor=['source', 'template']), paths=dict(), source=dict(copyfile=True, field='subj.source', mandatory=True, xor=['parameter_file']), source_image_smoothing=dict(field='eoptions.smosrc'), source_weight=dict(copyfile=False, extensions=None, field='subj.wtsrc'), template=dict(copyfile=False, extensions=None, field='eoptions.template', mandatory=True, xor=['parameter_file']), template_image_smoothing=dict(field='eoptions.smoref'), template_weight=dict(copyfile=False, extensions=None, field='eoptions.weight'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), write_bounding_box=dict(field='roptions.bb'), write_interp=dict(field='roptions.interp'), write_preserve=dict(field='roptions.preserve'), write_voxel_sizes=dict(field='roptions.vox'), write_wrap=dict(field='roptions.wrap'))
```

## Next Steps


---

*Source: test_auto_Normalize.py:6 | Complexity: Beginner | Last updated: 2026-05-18*