# How To: Warputils Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test WarpUtils inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='--in=%s', extensions=None, mandatory=True), knot_space=dict(argstr='--knotspace=%d,%d,%d'), out_file=dict(argstr='--out=%s', extensions=None, name_source=['in_file'], output_name='out_file', position=-1), out_format=dict(argstr='--outformat=%s'), out_jacobian=dict(argstr='--jac=%s', extensions=None), output_type=dict(), reference=dict(argstr='--ref=%s', extensions=None, mandatory=True), warp_resolution=dict(argstr='--warpres=%0.4f,%0.4f,%0.4f'), with_affine=dict(argstr='--withaff'), write_jacobian=dict(mandatory=True, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='--in=%s', extensions=None, mandatory=True), knot_space=dict(argstr='--knotspace=%d,%d,%d'), out_file=dict(argstr='--out=%s', extensions=None, name_source=['in_file'], output_name='out_file', position=-1), out_format=dict(argstr='--outformat=%s'), out_jacobian=dict(argstr='--jac=%s', extensions=None), output_type=dict(), reference=dict(argstr='--ref=%s', extensions=None, mandatory=True), warp_resolution=dict(argstr='--warpres=%0.4f,%0.4f,%0.4f'), with_affine=dict(argstr='--withaff'), write_jacobian=dict(mandatory=True, usedefault=True))
```

## Next Steps


---

*Source: test_auto_WarpUtils.py:6 | Complexity: Beginner | Last updated: 2026-05-18*