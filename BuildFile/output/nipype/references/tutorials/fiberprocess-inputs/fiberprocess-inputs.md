# How To: Fiberprocess Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fiberprocess inputs

## Prerequisites

**Required Modules:**
- `fiberprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), displacement_field=dict(argstr='--displacement_field %s', extensions=None), environ=dict(nohash=True, usedefault=True), fiber_file=dict(argstr='--fiber_file %s', extensions=None), fiber_output=dict(argstr='--fiber_output %s', hash_files=False), fiber_radius=dict(argstr='--fiber_radius %f'), h_field=dict(argstr='--h_field %s', extensions=None), index_space=dict(argstr='--index_space '), noDataChange=dict(argstr='--noDataChange '), no_warp=dict(argstr='--no_warp '), saveProperties=dict(argstr='--saveProperties '), tensor_volume=dict(argstr='--tensor_volume %s', extensions=None), verbose=dict(argstr='--verbose '), voxel_label=dict(argstr='--voxel_label %d'), voxelize=dict(argstr='--voxelize %s', hash_files=False), voxelize_count_fibers=dict(argstr='--voxelize_count_fibers '))
```

**Verification:**
```python
assert getattr(inputs.traits()[key], metakey) == value
```

### Step 2: Assign inputs = fiberprocess.input_spec(...)

```python
inputs = fiberprocess.input_spec()
```

**Verification:**
```python
assert getattr(inputs.traits()[key], metakey) == value
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), displacement_field=dict(argstr='--displacement_field %s', extensions=None), environ=dict(nohash=True, usedefault=True), fiber_file=dict(argstr='--fiber_file %s', extensions=None), fiber_output=dict(argstr='--fiber_output %s', hash_files=False), fiber_radius=dict(argstr='--fiber_radius %f'), h_field=dict(argstr='--h_field %s', extensions=None), index_space=dict(argstr='--index_space '), noDataChange=dict(argstr='--noDataChange '), no_warp=dict(argstr='--no_warp '), saveProperties=dict(argstr='--saveProperties '), tensor_volume=dict(argstr='--tensor_volume %s', extensions=None), verbose=dict(argstr='--verbose '), voxel_label=dict(argstr='--voxel_label %d'), voxelize=dict(argstr='--voxelize %s', hash_files=False), voxelize_count_fibers=dict(argstr='--voxelize_count_fibers '))
inputs = fiberprocess.input_spec()
for key, metadata in list(input_map.items()):
    for metakey, value in list(metadata.items()):
        assert getattr(inputs.traits()[key], metakey) == value
```

## Next Steps


---

*Source: test_auto_fiberprocess.py:5 | Complexity: Beginner | Last updated: 2026-05-18*