# How To: Createtiledmosaic Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CreateTiledMosaic inputs

## Prerequisites

**Required Modules:**
- `visualization`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(alpha_value=dict(argstr='-a %.2f'), args=dict(argstr='%s'), direction=dict(argstr='-d %d'), environ=dict(nohash=True, usedefault=True), flip_slice=dict(argstr='-f %s'), input_image=dict(argstr='-i %s', extensions=None, mandatory=True), mask_image=dict(argstr='-x %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='-o %s', usedefault=True), pad_or_crop=dict(argstr='-p %s'), permute_axes=dict(argstr='-g'), rgb_image=dict(argstr='-r %s', extensions=None, mandatory=True), slices=dict(argstr='-s %s'), tile_geometry=dict(argstr='-t %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(alpha_value=dict(argstr='-a %.2f'), args=dict(argstr='%s'), direction=dict(argstr='-d %d'), environ=dict(nohash=True, usedefault=True), flip_slice=dict(argstr='-f %s'), input_image=dict(argstr='-i %s', extensions=None, mandatory=True), mask_image=dict(argstr='-x %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='-o %s', usedefault=True), pad_or_crop=dict(argstr='-p %s'), permute_axes=dict(argstr='-g'), rgb_image=dict(argstr='-r %s', extensions=None, mandatory=True), slices=dict(argstr='-s %s'), tile_geometry=dict(argstr='-t %s'))
```

## Next Steps


---

*Source: test_auto_CreateTiledMosaic.py:6 | Complexity: Beginner | Last updated: 2026-05-18*