# How To: Imagemeants Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ImageMeants inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), eig=dict(argstr='--eig'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=0), mask=dict(argstr='-m %s', extensions=None), nobin=dict(argstr='--no_bin'), order=dict(argstr='--order=%d', usedefault=True), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), output_type=dict(), show_all=dict(argstr='--showall'), spatial_coord=dict(argstr='-c %s'), transpose=dict(argstr='--transpose'), use_mm=dict(argstr='--usemm'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), eig=dict(argstr='--eig'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=0), mask=dict(argstr='-m %s', extensions=None), nobin=dict(argstr='--no_bin'), order=dict(argstr='--order=%d', usedefault=True), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), output_type=dict(), show_all=dict(argstr='--showall'), spatial_coord=dict(argstr='-c %s'), transpose=dict(argstr='--transpose'), use_mm=dict(argstr='--usemm'))
```

## Next Steps


---

*Source: test_auto_ImageMeants.py:6 | Complexity: Beginner | Last updated: 2026-05-18*