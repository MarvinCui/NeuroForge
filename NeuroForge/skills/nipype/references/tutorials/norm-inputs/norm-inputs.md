# How To: Norm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Norm inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), clamp=dict(argstr='-clamp', usedefault=True), clobber=dict(argstr='-clobber', usedefault=True), cutoff=dict(argstr='-cutoff %s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), lower=dict(argstr='-lower %s'), mask=dict(argstr='-mask %s', extensions=None), out_ceil=dict(argstr='-out_ceil %s'), out_floor=dict(argstr='-out_floor %s'), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_norm.mnc', position=-1), output_threshold_mask=dict(argstr='-threshold_mask %s', extensions=None, hash_files=False, name_source=['input_file'], name_template='%s_norm_threshold_mask.mnc'), threshold=dict(argstr='-threshold'), threshold_blur=dict(argstr='-threshold_blur %s'), threshold_bmt=dict(argstr='-threshold_bmt'), threshold_perc=dict(argstr='-threshold_perc %s'), upper=dict(argstr='-upper %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), clamp=dict(argstr='-clamp', usedefault=True), clobber=dict(argstr='-clobber', usedefault=True), cutoff=dict(argstr='-cutoff %s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), lower=dict(argstr='-lower %s'), mask=dict(argstr='-mask %s', extensions=None), out_ceil=dict(argstr='-out_ceil %s'), out_floor=dict(argstr='-out_floor %s'), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_norm.mnc', position=-1), output_threshold_mask=dict(argstr='-threshold_mask %s', extensions=None, hash_files=False, name_source=['input_file'], name_template='%s_norm_threshold_mask.mnc'), threshold=dict(argstr='-threshold'), threshold_blur=dict(argstr='-threshold_blur %s'), threshold_bmt=dict(argstr='-threshold_bmt'), threshold_perc=dict(argstr='-threshold_perc %s'), upper=dict(argstr='-upper %s'))
```

## Next Steps


---

*Source: test_auto_Norm.py:6 | Complexity: Beginner | Last updated: 2026-05-18*