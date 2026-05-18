# How To: Mtnormalise Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MTNormalise inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), csf_fod=dict(argstr='%s', extensions=None, position=5), environ=dict(nohash=True, usedefault=True), gm_fod=dict(argstr='%s', extensions=None, position=3), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), mask=dict(argstr='-mask %s', extensions=None, position=-1), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file_csf=dict(argstr='%s', extensions=None, position=6), out_file_gm=dict(argstr='%s', extensions=None, position=4), out_file_wm=dict(argstr='%s', extensions=None, position=2), wm_fod=dict(argstr='%s', extensions=None, position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), csf_fod=dict(argstr='%s', extensions=None, position=5), environ=dict(nohash=True, usedefault=True), gm_fod=dict(argstr='%s', extensions=None, position=3), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), mask=dict(argstr='-mask %s', extensions=None, position=-1), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file_csf=dict(argstr='%s', extensions=None, position=6), out_file_gm=dict(argstr='%s', extensions=None, position=4), out_file_wm=dict(argstr='%s', extensions=None, position=2), wm_fod=dict(argstr='%s', extensions=None, position=1))
```

## Next Steps


---

*Source: test_auto_MTNormalise.py:6 | Complexity: Beginner | Last updated: 2026-05-18*