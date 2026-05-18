# How To: Warpimagemultitransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test WarpImageMultiTransform inputs

## Prerequisites

**Required Modules:**
- `resampling`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', extensions=None, mandatory=True, position=2), invert_affine=dict(), num_threads=dict(nohash=True, usedefault=True), out_postfix=dict(extensions=None, hash_files=False, usedefault=True, xor=['output_image']), output_image=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=3, xor=['out_postfix']), reference_image=dict(argstr='-R %s', extensions=None, xor=['tightest_box']), reslice_by_header=dict(argstr='--reslice-by-header'), tightest_box=dict(argstr='--tightest-bounding-box', xor=['reference_image']), transformation_series=dict(argstr='%s', mandatory=True, position=-1), use_bspline=dict(argstr='--use-BSpline'), use_nearest=dict(argstr='--use-NN'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', extensions=None, mandatory=True, position=2), invert_affine=dict(), num_threads=dict(nohash=True, usedefault=True), out_postfix=dict(extensions=None, hash_files=False, usedefault=True, xor=['output_image']), output_image=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=3, xor=['out_postfix']), reference_image=dict(argstr='-R %s', extensions=None, xor=['tightest_box']), reslice_by_header=dict(argstr='--reslice-by-header'), tightest_box=dict(argstr='--tightest-bounding-box', xor=['reference_image']), transformation_series=dict(argstr='%s', mandatory=True, position=-1), use_bspline=dict(argstr='--use-BSpline'), use_nearest=dict(argstr='--use-NN'))
```

## Next Steps


---

*Source: test_auto_WarpImageMultiTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*