# How To: C3D Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test C3d inputs

## Prerequisites

**Required Modules:**
- `c3`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', mandatory=True, position=1), interp=dict(argstr='-interpolation %s'), is_4d=dict(usedefault=True), multicomp_split=dict(argstr='-mcr', position=0, usedefault=True), out_file=dict(argstr='-o %s', extensions=None, position=-1, xor=['out_files']), out_files=dict(argstr='-oo %s', position=-1, xor=['out_file']), pix_type=dict(argstr='-type %s'), resample=dict(argstr='-resample %s'), scale=dict(argstr='-scale %s'), shift=dict(argstr='-shift %s'), smooth=dict(argstr='-smooth %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', mandatory=True, position=1), interp=dict(argstr='-interpolation %s'), is_4d=dict(usedefault=True), multicomp_split=dict(argstr='-mcr', position=0, usedefault=True), out_file=dict(argstr='-o %s', extensions=None, position=-1, xor=['out_files']), out_files=dict(argstr='-oo %s', position=-1, xor=['out_file']), pix_type=dict(argstr='-type %s'), resample=dict(argstr='-resample %s'), scale=dict(argstr='-scale %s'), shift=dict(argstr='-shift %s'), smooth=dict(argstr='-smooth %s'))
```

## Next Steps


---

*Source: test_auto_C3d.py:6 | Complexity: Beginner | Last updated: 2026-05-18*