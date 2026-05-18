# How To: Warptimeseriesimagemultitransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test WarpTimeSeriesImageMultiTransform inputs

## Prerequisites

**Required Modules:**
- `resampling`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True), invert_affine=dict(), num_threads=dict(nohash=True, usedefault=True), out_postfix=dict(argstr='%s', usedefault=True), reference_image=dict(argstr='-R %s', extensions=None, xor=['tightest_box']), reslice_by_header=dict(argstr='--reslice-by-header'), tightest_box=dict(argstr='--tightest-bounding-box', xor=['reference_image']), transformation_series=dict(argstr='%s', copyfile=False, mandatory=True), use_bspline=dict(argstr='--use-Bspline'), use_nearest=dict(argstr='--use-NN'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True), invert_affine=dict(), num_threads=dict(nohash=True, usedefault=True), out_postfix=dict(argstr='%s', usedefault=True), reference_image=dict(argstr='-R %s', extensions=None, xor=['tightest_box']), reslice_by_header=dict(argstr='--reslice-by-header'), tightest_box=dict(argstr='--tightest-bounding-box', xor=['reference_image']), transformation_series=dict(argstr='%s', copyfile=False, mandatory=True), use_bspline=dict(argstr='--use-Bspline'), use_nearest=dict(argstr='--use-NN'))
```

## Next Steps


---

*Source: test_auto_WarpTimeSeriesImageMultiTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*