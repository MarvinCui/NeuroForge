# How To: Buildconnectome Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BuildConnectome inputs

## Prerequisites

**Required Modules:**
- `connectivity`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), in_parc=dict(argstr='%s', extensions=None, position=-2), in_scalar=dict(argstr='-image %s', extensions=None), in_weights=dict(argstr='-tck_weights_in %s', extensions=None), keep_unassigned=dict(argstr='-keep_unassigned'), metric=dict(argstr='-metric %s'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), search_forward=dict(argstr='-assignment_forward_search %f'), search_radius=dict(argstr='-assignment_radial_search %f'), search_reverse=dict(argstr='-assignment_reverse_search %f'), vox_lookup=dict(argstr='-assignment_voxel_lookup'), zero_diagonal=dict(argstr='-zero_diagonal'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), in_parc=dict(argstr='%s', extensions=None, position=-2), in_scalar=dict(argstr='-image %s', extensions=None), in_weights=dict(argstr='-tck_weights_in %s', extensions=None), keep_unassigned=dict(argstr='-keep_unassigned'), metric=dict(argstr='-metric %s'), nthreads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), search_forward=dict(argstr='-assignment_forward_search %f'), search_radius=dict(argstr='-assignment_radial_search %f'), search_reverse=dict(argstr='-assignment_reverse_search %f'), vox_lookup=dict(argstr='-assignment_voxel_lookup'), zero_diagonal=dict(argstr='-zero_diagonal'))
```

## Next Steps


---

*Source: test_auto_BuildConnectome.py:6 | Complexity: Beginner | Last updated: 2026-05-18*