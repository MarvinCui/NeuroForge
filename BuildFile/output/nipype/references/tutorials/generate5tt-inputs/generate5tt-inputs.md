# How To: Generate5Tt Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Generate5tt inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(algorithm=dict(argstr='%s', mandatory=True, position=-3), args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), hippocampi=dict(argstr='-hippocampi %s'), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', mandatory=True, position=-2), lut_file=dict(argstr='-lut %s', extensions=None), mask_file=dict(argstr='-mask %s', extensions=None), nocrop=dict(argstr='-nocrop'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), premasked=dict(argstr='-premasked'), sgm_amyg_hipp=dict(argstr='-sgm_amyg_hipp'), t2_image=dict(argstr='-t2 %s', extensions=None), template=dict(argstr='-template %s', extensions=None), white_stem=dict(argstr='-white_stem'))
```


## Complete Example

```python
# Workflow
input_map = dict(algorithm=dict(argstr='%s', mandatory=True, position=-3), args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), hippocampi=dict(argstr='-hippocampi %s'), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', mandatory=True, position=-2), lut_file=dict(argstr='-lut %s', extensions=None), mask_file=dict(argstr='-mask %s', extensions=None), nocrop=dict(argstr='-nocrop'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), premasked=dict(argstr='-premasked'), sgm_amyg_hipp=dict(argstr='-sgm_amyg_hipp'), t2_image=dict(argstr='-t2 %s', extensions=None), template=dict(argstr='-template %s', extensions=None), white_stem=dict(argstr='-white_stem'))
```

## Next Steps


---

*Source: test_auto_Generate5tt.py:6 | Complexity: Beginner | Last updated: 2026-05-18*