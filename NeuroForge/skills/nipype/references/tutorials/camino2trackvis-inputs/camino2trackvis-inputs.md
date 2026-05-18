# How To: Camino2Trackvis Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Camino2Trackvis inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), data_dims=dict(argstr='-d %s', mandatory=True, position=4, sep=','), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), min_length=dict(argstr='-l %d', position=3, units='mm'), nifti_file=dict(argstr='--nifti %s', extensions=None, position=7), out_file=dict(argstr='-o %s', extensions=None, genfile=True, position=2), voxel_dims=dict(argstr='-x %s', mandatory=True, position=5, sep=','), voxel_order=dict(argstr='--voxel-order %s', extensions=None, mandatory=True, position=6))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), data_dims=dict(argstr='-d %s', mandatory=True, position=4, sep=','), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), min_length=dict(argstr='-l %d', position=3, units='mm'), nifti_file=dict(argstr='--nifti %s', extensions=None, position=7), out_file=dict(argstr='-o %s', extensions=None, genfile=True, position=2), voxel_dims=dict(argstr='-x %s', mandatory=True, position=5, sep=','), voxel_order=dict(argstr='--voxel-order %s', extensions=None, mandatory=True, position=6))
```

## Next Steps


---

*Source: test_auto_Camino2Trackvis.py:6 | Complexity: Beginner | Last updated: 2026-05-18*