# How To: Tck2Vtk Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TCK2VTK inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), nthreads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, position=-1, usedefault=True), reference=dict(argstr='-image %s', extensions=None), voxel=dict(argstr='-image %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), nthreads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, position=-1, usedefault=True), reference=dict(argstr='-image %s', extensions=None), voxel=dict(argstr='-image %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_TCK2VTK.py:6 | Complexity: Beginner | Last updated: 2026-05-18*