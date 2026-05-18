# How To: Fittensor Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FitTensor inputs

## Prerequisites

**Required Modules:**
- `reconst`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), in_mask=dict(argstr='-mask %s', extensions=None), method=dict(argstr='-method %s'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), predicted_signal=dict(argstr='-predicted_signal %s', extensions=None), reg_term=dict(argstr='-regularisation %f', max_ver='0.3.13'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), in_mask=dict(argstr='-mask %s', extensions=None), method=dict(argstr='-method %s'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), predicted_signal=dict(argstr='-predicted_signal %s', extensions=None), reg_term=dict(argstr='-regularisation %f', max_ver='0.3.13'))
```

## Next Steps


---

*Source: test_auto_FitTensor.py:6 | Complexity: Beginner | Last updated: 2026-05-18*