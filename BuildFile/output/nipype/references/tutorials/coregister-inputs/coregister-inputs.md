# How To: Coregister Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Coregister inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(apply_to_files=dict(copyfile=True, field='other'), cost_function=dict(field='eoptions.cost_fun'), fwhm=dict(field='eoptions.fwhm'), jobtype=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='roptions.prefix', usedefault=True), paths=dict(), separation=dict(field='eoptions.sep'), source=dict(copyfile=True, field='source', mandatory=True), target=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='ref', mandatory=True), tolerance=dict(field='eoptions.tol'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), write_interp=dict(field='roptions.interp'), write_mask=dict(field='roptions.mask'), write_wrap=dict(field='roptions.wrap'))
```


## Complete Example

```python
# Workflow
input_map = dict(apply_to_files=dict(copyfile=True, field='other'), cost_function=dict(field='eoptions.cost_fun'), fwhm=dict(field='eoptions.fwhm'), jobtype=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='roptions.prefix', usedefault=True), paths=dict(), separation=dict(field='eoptions.sep'), source=dict(copyfile=True, field='source', mandatory=True), target=dict(copyfile=False, extensions=['.hdr', '.img', '.img.gz', '.nii'], field='ref', mandatory=True), tolerance=dict(field='eoptions.tol'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), write_interp=dict(field='roptions.interp'), write_mask=dict(field='roptions.mask'), write_wrap=dict(field='roptions.wrap'))
```

## Next Steps


---

*Source: test_auto_Coregister.py:6 | Complexity: Beginner | Last updated: 2026-05-18*