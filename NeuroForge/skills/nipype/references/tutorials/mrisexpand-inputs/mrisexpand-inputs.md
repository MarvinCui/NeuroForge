# How To: Mrisexpand Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRIsExpand inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), distance=dict(argstr='%g', mandatory=True, position=-2), dt=dict(argstr='-T %g'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-3), nsurfaces=dict(argstr='-N %d'), out_name=dict(argstr='%s', position=-1, usedefault=True), pial=dict(argstr='-pial %s', copyfile=False), smooth_averages=dict(argstr='-A %d'), sphere=dict(copyfile=False, usedefault=True), spring=dict(argstr='-S %g'), subjects_dir=dict(), thickness=dict(argstr='-thickness'), thickness_name=dict(argstr='-thickness_name %s', copyfile=False), write_iterations=dict(argstr='-W %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), distance=dict(argstr='%g', mandatory=True, position=-2), dt=dict(argstr='-T %g'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-3), nsurfaces=dict(argstr='-N %d'), out_name=dict(argstr='%s', position=-1, usedefault=True), pial=dict(argstr='-pial %s', copyfile=False), smooth_averages=dict(argstr='-A %d'), sphere=dict(copyfile=False, usedefault=True), spring=dict(argstr='-S %g'), subjects_dir=dict(), thickness=dict(argstr='-thickness'), thickness_name=dict(argstr='-thickness_name %s', copyfile=False), write_iterations=dict(argstr='-W %d'))
```

## Next Steps


---

*Source: test_auto_MRIsExpand.py:6 | Complexity: Beginner | Last updated: 2026-05-18*