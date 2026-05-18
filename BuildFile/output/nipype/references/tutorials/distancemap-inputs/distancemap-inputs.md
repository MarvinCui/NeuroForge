# How To: Distancemap Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DistanceMap inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), distance_map=dict(argstr='--out=%s', extensions=None, genfile=True, hash_files=False), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='--in=%s', extensions=None, mandatory=True), invert_input=dict(argstr='--invert'), local_max_file=dict(argstr='--localmax=%s', hash_files=False), mask_file=dict(argstr='--mask=%s', extensions=None), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), distance_map=dict(argstr='--out=%s', extensions=None, genfile=True, hash_files=False), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='--in=%s', extensions=None, mandatory=True), invert_input=dict(argstr='--invert'), local_max_file=dict(argstr='--localmax=%s', hash_files=False), mask_file=dict(argstr='--mask=%s', extensions=None), output_type=dict())
```

## Next Steps


---

*Source: test_auto_DistanceMap.py:6 | Complexity: Beginner | Last updated: 2026-05-18*