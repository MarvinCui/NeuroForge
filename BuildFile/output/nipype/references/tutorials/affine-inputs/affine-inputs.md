# How To: Affine Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Affine inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixed_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=0), ftol=dict(argstr='%g', mandatory=True, position=4, usedefault=True), initialize_xfm=dict(argstr='%s', copyfile=True, extensions=None, position=5), moving_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=1), sampling_xyz=dict(argstr='%g %g %g', mandatory=True, position=3, usedefault=True), similarity_metric=dict(argstr='%s', mandatory=True, position=2, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixed_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=0), ftol=dict(argstr='%g', mandatory=True, position=4, usedefault=True), initialize_xfm=dict(argstr='%s', copyfile=True, extensions=None, position=5), moving_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=1), sampling_xyz=dict(argstr='%g %g %g', mandatory=True, position=3, usedefault=True), similarity_metric=dict(argstr='%s', mandatory=True, position=2, usedefault=True))
```

## Next Steps


---

*Source: test_auto_Affine.py:6 | Complexity: Beginner | Last updated: 2026-05-18*