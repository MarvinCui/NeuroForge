# How To: Mrdegibbs Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRDeGibbs inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), axes=dict(argstr='-axes %s', sep=',', usedefault=True), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), maxW=dict(argstr='-maxW %d', usedefault=True), minW=dict(argstr='-minW %d', usedefault=True), nshifts=dict(argstr='-nshifts %d', usedefault=True), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_unr', position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), axes=dict(argstr='-axes %s', sep=',', usedefault=True), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), maxW=dict(argstr='-maxW %d', usedefault=True), minW=dict(argstr='-minW %d', usedefault=True), nshifts=dict(argstr='-nshifts %d', usedefault=True), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_unr', position=-1))
```

## Next Steps


---

*Source: test_auto_MRDeGibbs.py:6 | Complexity: Beginner | Last updated: 2026-05-18*