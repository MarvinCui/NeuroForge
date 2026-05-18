# How To: Responsesd Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ResponseSD inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(algorithm=dict(argstr='%s', mandatory=True, position=1), args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), csf_file=dict(argstr='%s', extensions=None, position=-1), environ=dict(nohash=True, usedefault=True), gm_file=dict(argstr='%s', extensions=None, position=-2), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-5), in_mask=dict(argstr='-mask %s', extensions=None), max_sh=dict(argstr='-lmax %s', sep=','), mtt_file=dict(argstr='%s', extensions=None, position=-4), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), wm_file=dict(argstr='%s', extensions=None, position=-3, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(algorithm=dict(argstr='%s', mandatory=True, position=1), args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), csf_file=dict(argstr='%s', extensions=None, position=-1), environ=dict(nohash=True, usedefault=True), gm_file=dict(argstr='%s', extensions=None, position=-2), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-5), in_mask=dict(argstr='-mask %s', extensions=None), max_sh=dict(argstr='-lmax %s', sep=','), mtt_file=dict(argstr='%s', extensions=None, position=-4), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), wm_file=dict(argstr='%s', extensions=None, position=-3, usedefault=True))
```

## Next Steps


---

*Source: test_auto_ResponseSD.py:6 | Complexity: Beginner | Last updated: 2026-05-18*