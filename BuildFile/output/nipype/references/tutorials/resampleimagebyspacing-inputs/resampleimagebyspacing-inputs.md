# How To: Resampleimagebyspacing Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ResampleImageBySpacing inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(addvox=dict(argstr='%d', position=6, requires=['apply_smoothing']), apply_smoothing=dict(argstr='%d', position=5), args=dict(argstr='%s'), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', extensions=None, mandatory=True, position=2), nn_interp=dict(argstr='%d', position=-1, requires=['addvox']), num_threads=dict(nohash=True, usedefault=True), out_spacing=dict(argstr='%s', mandatory=True, position=4), output_image=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['input_image'], name_template='%s_resampled', position=3))
```


## Complete Example

```python
# Workflow
input_map = dict(addvox=dict(argstr='%d', position=6, requires=['apply_smoothing']), apply_smoothing=dict(argstr='%d', position=5), args=dict(argstr='%s'), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', extensions=None, mandatory=True, position=2), nn_interp=dict(argstr='%d', position=-1, requires=['addvox']), num_threads=dict(nohash=True, usedefault=True), out_spacing=dict(argstr='%s', mandatory=True, position=4), output_image=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['input_image'], name_template='%s_resampled', position=3))
```

## Next Steps


---

*Source: test_auto_ResampleImageBySpacing.py:6 | Complexity: Beginner | Last updated: 2026-05-18*