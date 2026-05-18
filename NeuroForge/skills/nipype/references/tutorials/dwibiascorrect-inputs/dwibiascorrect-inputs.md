# How To: Dwibiascorrect Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIBiasCorrect inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bias=dict(argstr='-bias %s', extensions=None), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), in_mask=dict(argstr='-mask %s', extensions=None), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, genfile=True, keep_extension=True, name_source='in_file', name_template='%s_biascorr', position=-1), use_ants=dict(argstr='ants', mandatory=True, position=0, xor=['use_fsl']), use_fsl=dict(argstr='fsl', mandatory=True, position=0, xor=['use_ants']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bias=dict(argstr='-bias %s', extensions=None), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), in_mask=dict(argstr='-mask %s', extensions=None), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, genfile=True, keep_extension=True, name_source='in_file', name_template='%s_biascorr', position=-1), use_ants=dict(argstr='ants', mandatory=True, position=0, xor=['use_fsl']), use_fsl=dict(argstr='fsl', mandatory=True, position=0, xor=['use_ants']))
```

## Next Steps


---

*Source: test_auto_DWIBiasCorrect.py:6 | Complexity: Beginner | Last updated: 2026-05-18*