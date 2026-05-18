# How To: Vtkstreamlines Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test VtkStreamlines inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), colourorient=dict(argstr='-colourorient'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr=' < %s', extensions=None, mandatory=True, position=-2), inputmodel=dict(argstr='-inputmodel %s', usedefault=True), interpolate=dict(argstr='-interpolate'), interpolatescalars=dict(argstr='-interpolatescalars'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), scalar_file=dict(argstr='-scalarfile %s', extensions=None, position=3), seed_file=dict(argstr='-seedfile %s', extensions=None, position=1), target_file=dict(argstr='-targetfile %s', extensions=None, position=2), voxeldims=dict(argstr='-voxeldims %s', position=4, units='mm'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), colourorient=dict(argstr='-colourorient'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr=' < %s', extensions=None, mandatory=True, position=-2), inputmodel=dict(argstr='-inputmodel %s', usedefault=True), interpolate=dict(argstr='-interpolate'), interpolatescalars=dict(argstr='-interpolatescalars'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), scalar_file=dict(argstr='-scalarfile %s', extensions=None, position=3), seed_file=dict(argstr='-seedfile %s', extensions=None, position=1), target_file=dict(argstr='-targetfile %s', extensions=None, position=2), voxeldims=dict(argstr='-voxeldims %s', position=4, units='mm'))
```

## Next Steps


---

*Source: test_auto_VtkStreamlines.py:6 | Complexity: Beginner | Last updated: 2026-05-18*