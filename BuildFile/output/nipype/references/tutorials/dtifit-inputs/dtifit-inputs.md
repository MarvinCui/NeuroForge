# How To: Dtifit Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DTIFit inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), base_name=dict(argstr='-o %s', position=1, usedefault=True), bvals=dict(argstr='-b %s', extensions=None, mandatory=True, position=4), bvecs=dict(argstr='-r %s', extensions=None, mandatory=True, position=3), cni=dict(argstr='--cni=%s', extensions=None), dwi=dict(argstr='-k %s', extensions=None, mandatory=True, position=0), environ=dict(nohash=True, usedefault=True), gradnonlin=dict(argstr='--gradnonlin=%s', extensions=None), little_bit=dict(argstr='--littlebit'), mask=dict(argstr='-m %s', extensions=None, mandatory=True, position=2), max_x=dict(argstr='-X %d'), max_y=dict(argstr='-Y %d'), max_z=dict(argstr='-Z %d'), min_x=dict(argstr='-x %d'), min_y=dict(argstr='-y %d'), min_z=dict(argstr='-z %d'), output_type=dict(), save_tensor=dict(argstr='--save_tensor'), sse=dict(argstr='--sse'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), base_name=dict(argstr='-o %s', position=1, usedefault=True), bvals=dict(argstr='-b %s', extensions=None, mandatory=True, position=4), bvecs=dict(argstr='-r %s', extensions=None, mandatory=True, position=3), cni=dict(argstr='--cni=%s', extensions=None), dwi=dict(argstr='-k %s', extensions=None, mandatory=True, position=0), environ=dict(nohash=True, usedefault=True), gradnonlin=dict(argstr='--gradnonlin=%s', extensions=None), little_bit=dict(argstr='--littlebit'), mask=dict(argstr='-m %s', extensions=None, mandatory=True, position=2), max_x=dict(argstr='-X %d'), max_y=dict(argstr='-Y %d'), max_z=dict(argstr='-Z %d'), min_x=dict(argstr='-x %d'), min_y=dict(argstr='-y %d'), min_z=dict(argstr='-z %d'), output_type=dict(), save_tensor=dict(argstr='--save_tensor'), sse=dict(argstr='--sse'))
```

## Next Steps


---

*Source: test_auto_DTIFit.py:6 | Complexity: Beginner | Last updated: 2026-05-18*