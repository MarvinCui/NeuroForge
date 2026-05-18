# How To: Sphericalaverage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SphericalAverage inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), erode=dict(argstr='-erode %d'), fname=dict(argstr='%s', mandatory=True, position=-5), hemisphere=dict(argstr='%s', mandatory=True, position=-4), in_average=dict(argstr='%s', genfile=True, position=-2), in_orig=dict(argstr='-orig %s', extensions=None), in_surf=dict(argstr='%s', extensions=None, mandatory=True, position=-3), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), subject_id=dict(argstr='-o %s', mandatory=True), subjects_dir=dict(), threshold=dict(argstr='-t %.1f'), which=dict(argstr='%s', mandatory=True, position=-6))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), erode=dict(argstr='-erode %d'), fname=dict(argstr='%s', mandatory=True, position=-5), hemisphere=dict(argstr='%s', mandatory=True, position=-4), in_average=dict(argstr='%s', genfile=True, position=-2), in_orig=dict(argstr='-orig %s', extensions=None), in_surf=dict(argstr='%s', extensions=None, mandatory=True, position=-3), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), subject_id=dict(argstr='-o %s', mandatory=True), subjects_dir=dict(), threshold=dict(argstr='-t %.1f'), which=dict(argstr='%s', mandatory=True, position=-6))
```

## Next Steps


---

*Source: test_auto_SphericalAverage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*