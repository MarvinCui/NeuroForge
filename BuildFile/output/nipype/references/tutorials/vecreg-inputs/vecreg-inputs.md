# How To: Vecreg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test VecReg inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(affine_mat=dict(argstr='-t %s', extensions=None), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), interpolation=dict(argstr='--interp=%s'), mask=dict(argstr='-m %s', extensions=None), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), output_type=dict(), ref_mask=dict(argstr='--refmask=%s', extensions=None), ref_vol=dict(argstr='-r %s', extensions=None, mandatory=True), rotation_mat=dict(argstr='--rotmat=%s', extensions=None), rotation_warp=dict(argstr='--rotwarp=%s', extensions=None), warp_field=dict(argstr='-w %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(affine_mat=dict(argstr='-t %s', extensions=None), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), interpolation=dict(argstr='--interp=%s'), mask=dict(argstr='-m %s', extensions=None), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), output_type=dict(), ref_mask=dict(argstr='--refmask=%s', extensions=None), ref_vol=dict(argstr='-r %s', extensions=None, mandatory=True), rotation_mat=dict(argstr='--rotmat=%s', extensions=None), rotation_warp=dict(argstr='--rotwarp=%s', extensions=None), warp_field=dict(argstr='-w %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_VecReg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*