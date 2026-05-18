# How To: Dtitracker Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DTITracker inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(angle_threshold=dict(argstr='-at %f'), angle_threshold_weight=dict(argstr='-atw %f'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), input_data_prefix=dict(argstr='%s', position=0, usedefault=True), input_type=dict(argstr='-it %s'), invert_x=dict(argstr='-ix'), invert_y=dict(argstr='-iy'), invert_z=dict(argstr='-iz'), mask1_file=dict(argstr='-m %s', extensions=None, mandatory=True, position=2), mask1_threshold=dict(position=3), mask2_file=dict(argstr='-m2 %s', extensions=None, position=4), mask2_threshold=dict(position=5), output_file=dict(argstr='%s', extensions=None, position=1, usedefault=True), output_mask=dict(argstr='-om %s', extensions=None), primary_vector=dict(argstr='-%s'), random_seed=dict(argstr='-rseed %d'), step_length=dict(argstr='-l %f'), swap_xy=dict(argstr='-sxy'), swap_yz=dict(argstr='-syz'), swap_zx=dict(argstr='-szx'), tensor_file=dict(extensions=None), tracking_method=dict(argstr='-%s'))
```


## Complete Example

```python
# Workflow
input_map = dict(angle_threshold=dict(argstr='-at %f'), angle_threshold_weight=dict(argstr='-atw %f'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), input_data_prefix=dict(argstr='%s', position=0, usedefault=True), input_type=dict(argstr='-it %s'), invert_x=dict(argstr='-ix'), invert_y=dict(argstr='-iy'), invert_z=dict(argstr='-iz'), mask1_file=dict(argstr='-m %s', extensions=None, mandatory=True, position=2), mask1_threshold=dict(position=3), mask2_file=dict(argstr='-m2 %s', extensions=None, position=4), mask2_threshold=dict(position=5), output_file=dict(argstr='%s', extensions=None, position=1, usedefault=True), output_mask=dict(argstr='-om %s', extensions=None), primary_vector=dict(argstr='-%s'), random_seed=dict(argstr='-rseed %d'), step_length=dict(argstr='-l %f'), swap_xy=dict(argstr='-sxy'), swap_yz=dict(argstr='-syz'), swap_zx=dict(argstr='-szx'), tensor_file=dict(extensions=None), tracking_method=dict(argstr='-%s'))
```

## Next Steps


---

*Source: test_auto_DTITracker.py:6 | Complexity: Beginner | Last updated: 2026-05-18*