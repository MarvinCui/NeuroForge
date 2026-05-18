# How To: Smoothtessellation Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SmoothTessellation inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), curvature_averaging_iterations=dict(argstr='-a %d'), disable_estimates=dict(argstr='-nw'), environ=dict(nohash=True, usedefault=True), gaussian_curvature_norm_steps=dict(argstr='%d'), gaussian_curvature_smoothing_steps=dict(argstr=' %d'), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), normalize_area=dict(argstr='-area'), out_area_file=dict(argstr='-b %s', extensions=None), out_curvature_file=dict(argstr='-c %s', extensions=None), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), seed=dict(argstr='-seed %d'), smoothing_iterations=dict(argstr='-n %d'), snapshot_writing_iterations=dict(argstr='-w %d'), subjects_dir=dict(), use_gaussian_curvature_smoothing=dict(argstr='-g'), use_momentum=dict(argstr='-m'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), curvature_averaging_iterations=dict(argstr='-a %d'), disable_estimates=dict(argstr='-nw'), environ=dict(nohash=True, usedefault=True), gaussian_curvature_norm_steps=dict(argstr='%d'), gaussian_curvature_smoothing_steps=dict(argstr=' %d'), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), normalize_area=dict(argstr='-area'), out_area_file=dict(argstr='-b %s', extensions=None), out_curvature_file=dict(argstr='-c %s', extensions=None), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), seed=dict(argstr='-seed %d'), smoothing_iterations=dict(argstr='-n %d'), snapshot_writing_iterations=dict(argstr='-w %d'), subjects_dir=dict(), use_gaussian_curvature_smoothing=dict(argstr='-g'), use_momentum=dict(argstr='-m'))
```

## Next Steps


---

*Source: test_auto_SmoothTessellation.py:6 | Complexity: Beginner | Last updated: 2026-05-18*