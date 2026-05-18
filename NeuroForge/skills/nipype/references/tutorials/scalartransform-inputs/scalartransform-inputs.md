# How To: Scalartransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test scalartransform inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), deformation=dict(argstr='--deformation %s', extensions=None), environ=dict(nohash=True, usedefault=True), h_field=dict(argstr='--h_field '), input_image=dict(argstr='--input_image %s', extensions=None), interpolation=dict(argstr='--interpolation %s'), invert=dict(argstr='--invert '), output_image=dict(argstr='--output_image %s', hash_files=False), transformation=dict(argstr='--transformation %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), deformation=dict(argstr='--deformation %s', extensions=None), environ=dict(nohash=True, usedefault=True), h_field=dict(argstr='--h_field '), input_image=dict(argstr='--input_image %s', extensions=None), interpolation=dict(argstr='--interpolation %s'), invert=dict(argstr='--invert '), output_image=dict(argstr='--output_image %s', hash_files=False), transformation=dict(argstr='--transformation %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_scalartransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*