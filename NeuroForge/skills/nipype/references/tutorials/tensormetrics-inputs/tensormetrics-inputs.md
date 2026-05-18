# How To: Tensormetrics Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TensorMetrics inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), component=dict(argstr='-num %s', sep=',', usedefault=True), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), in_mask=dict(argstr='-mask %s', extensions=None), modulate=dict(argstr='-modulate %s'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_ad=dict(argstr='-ad %s', extensions=None), out_adc=dict(argstr='-adc %s', extensions=None), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_cl=dict(argstr='-cl %s', extensions=None), out_cp=dict(argstr='-cp %s', extensions=None), out_cs=dict(argstr='-cs %s', extensions=None), out_eval=dict(argstr='-value %s', extensions=None), out_evec=dict(argstr='-vector %s', extensions=None), out_fa=dict(argstr='-fa %s', extensions=None), out_rd=dict(argstr='-rd %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), component=dict(argstr='-num %s', sep=',', usedefault=True), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), in_mask=dict(argstr='-mask %s', extensions=None), modulate=dict(argstr='-modulate %s'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_ad=dict(argstr='-ad %s', extensions=None), out_adc=dict(argstr='-adc %s', extensions=None), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_cl=dict(argstr='-cl %s', extensions=None), out_cp=dict(argstr='-cp %s', extensions=None), out_cs=dict(argstr='-cs %s', extensions=None), out_eval=dict(argstr='-value %s', extensions=None), out_evec=dict(argstr='-vector %s', extensions=None), out_fa=dict(argstr='-fa %s', extensions=None), out_rd=dict(argstr='-rd %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_TensorMetrics.py:6 | Complexity: Beginner | Last updated: 2026-05-18*