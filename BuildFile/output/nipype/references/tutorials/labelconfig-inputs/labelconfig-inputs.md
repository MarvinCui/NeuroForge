# How To: Labelconfig Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test LabelConfig inputs

## Prerequisites

**Required Modules:**
- `connectivity`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_config=dict(argstr='%s', extensions=None, position=-2), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), lut_aal=dict(argstr='-lut_aal %s', extensions=None), lut_basic=dict(argstr='-lut_basic %s', extensions=None), lut_fs=dict(argstr='-lut_freesurfer %s', extensions=None), lut_itksnap=dict(argstr='-lut_itksnap %s', extensions=None), nthreads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), spine=dict(argstr='-spine %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_config=dict(argstr='%s', extensions=None, position=-2), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), lut_aal=dict(argstr='-lut_aal %s', extensions=None), lut_basic=dict(argstr='-lut_basic %s', extensions=None), lut_fs=dict(argstr='-lut_freesurfer %s', extensions=None), lut_itksnap=dict(argstr='-lut_itksnap %s', extensions=None), nthreads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), spine=dict(argstr='-spine %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_LabelConfig.py:6 | Complexity: Beginner | Last updated: 2026-05-18*