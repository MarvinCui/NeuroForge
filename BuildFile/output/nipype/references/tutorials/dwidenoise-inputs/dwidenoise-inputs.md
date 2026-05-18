# How To: Dwidenoise Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIDenoise inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), extent=dict(argstr='-extent %d,%d,%d'), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), mask=dict(argstr='-mask %s', extensions=None, position=1), noise=dict(argstr='-noise %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_noise'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_denoised', position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), extent=dict(argstr='-extent %d,%d,%d'), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), mask=dict(argstr='-mask %s', extensions=None, position=1), noise=dict(argstr='-noise %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_noise'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_denoised', position=-1))
```

## Next Steps


---

*Source: test_auto_DWIDenoise.py:6 | Complexity: Beginner | Last updated: 2026-05-18*