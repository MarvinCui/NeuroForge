# How To: Laplacianthickness Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test LaplacianThickness inputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dT=dict(argstr='%s', position=6, requires=['prior_thickness']), environ=dict(nohash=True, usedefault=True), input_gm=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=2), input_wm=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=1), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='%s', hash_files=False, keep_extension=True, name_source=['input_wm'], name_template='%s_thickness', position=3), prior_thickness=dict(argstr='%s', position=5, requires=['smooth_param']), smooth_param=dict(argstr='%s', position=4), sulcus_prior=dict(argstr='%s', position=7, requires=['dT']), tolerance=dict(argstr='%s', position=8, requires=['sulcus_prior']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dT=dict(argstr='%s', position=6, requires=['prior_thickness']), environ=dict(nohash=True, usedefault=True), input_gm=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=2), input_wm=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=1), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='%s', hash_files=False, keep_extension=True, name_source=['input_wm'], name_template='%s_thickness', position=3), prior_thickness=dict(argstr='%s', position=5, requires=['smooth_param']), smooth_param=dict(argstr='%s', position=4), sulcus_prior=dict(argstr='%s', position=7, requires=['dT']), tolerance=dict(argstr='%s', position=8, requires=['sulcus_prior']))
```

## Next Steps


---

*Source: test_auto_LaplacianThickness.py:6 | Complexity: Beginner | Last updated: 2026-05-18*