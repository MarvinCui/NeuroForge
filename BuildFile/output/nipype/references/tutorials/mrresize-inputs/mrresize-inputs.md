# How To: Mrresize Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRResize inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), image_size=dict(argstr='-size %d,%d,%d', mandatory=True, xor=['voxel_size', 'scale_factor']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), interpolation=dict(argstr='-interp %s', usedefault=True), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['in_file'], name_template='%s_resized', position=-1), scale_factor=dict(argstr='-scale %g,%g,%g', mandatory=True, xor=['image_size', 'voxel_size']), voxel_size=dict(argstr='-voxel %g,%g,%g', mandatory=True, xor=['image_size', 'scale_factor']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), image_size=dict(argstr='-size %d,%d,%d', mandatory=True, xor=['voxel_size', 'scale_factor']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), interpolation=dict(argstr='-interp %s', usedefault=True), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['in_file'], name_template='%s_resized', position=-1), scale_factor=dict(argstr='-scale %g,%g,%g', mandatory=True, xor=['image_size', 'voxel_size']), voxel_size=dict(argstr='-voxel %g,%g,%g', mandatory=True, xor=['image_size', 'scale_factor']))
```

## Next Steps


---

*Source: test_auto_MRResize.py:6 | Complexity: Beginner | Last updated: 2026-05-18*