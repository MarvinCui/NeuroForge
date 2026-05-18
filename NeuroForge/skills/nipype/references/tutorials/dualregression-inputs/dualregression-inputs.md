# How To: Dualregression Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DualRegression inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), con_file=dict(argstr='%s', extensions=None, position=4), des_norm=dict(argstr='%i', position=2, usedefault=True), design_file=dict(argstr='%s', extensions=None, position=3), environ=dict(nohash=True, usedefault=True), group_IC_maps_4D=dict(argstr='%s', extensions=None, mandatory=True, position=1), in_files=dict(argstr='%s', mandatory=True, position=-1, sep=' '), n_perm=dict(argstr='%i', mandatory=True, position=5), one_sample_group_mean=dict(argstr='-1', position=3), out_dir=dict(argstr='%s', genfile=True, position=6, usedefault=True), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), con_file=dict(argstr='%s', extensions=None, position=4), des_norm=dict(argstr='%i', position=2, usedefault=True), design_file=dict(argstr='%s', extensions=None, position=3), environ=dict(nohash=True, usedefault=True), group_IC_maps_4D=dict(argstr='%s', extensions=None, mandatory=True, position=1), in_files=dict(argstr='%s', mandatory=True, position=-1, sep=' '), n_perm=dict(argstr='%i', mandatory=True, position=5), one_sample_group_mean=dict(argstr='-1', position=3), out_dir=dict(argstr='%s', genfile=True, position=6, usedefault=True), output_type=dict())
```

## Next Steps


---

*Source: test_auto_DualRegression.py:6 | Complexity: Beginner | Last updated: 2026-05-18*