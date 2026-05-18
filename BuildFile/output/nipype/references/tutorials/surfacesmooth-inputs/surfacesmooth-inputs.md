# How To: Surfacesmooth Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SurfaceSmooth inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), cortex=dict(argstr='--cortex', usedefault=True), environ=dict(nohash=True, usedefault=True), fwhm=dict(argstr='--fwhm %.4f', xor=['smooth_iters']), hemi=dict(argstr='--hemi %s', mandatory=True), in_file=dict(argstr='--sval %s', extensions=None, mandatory=True), out_file=dict(argstr='--tval %s', extensions=None, genfile=True), reshape=dict(argstr='--reshape'), smooth_iters=dict(argstr='--smooth %d', xor=['fwhm']), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), cortex=dict(argstr='--cortex', usedefault=True), environ=dict(nohash=True, usedefault=True), fwhm=dict(argstr='--fwhm %.4f', xor=['smooth_iters']), hemi=dict(argstr='--hemi %s', mandatory=True), in_file=dict(argstr='--sval %s', extensions=None, mandatory=True), out_file=dict(argstr='--tval %s', extensions=None, genfile=True), reshape=dict(argstr='--reshape'), smooth_iters=dict(argstr='--smooth %d', xor=['fwhm']), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_SurfaceSmooth.py:6 | Complexity: Beginner | Last updated: 2026-05-18*