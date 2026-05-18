# How To: Mritessellate Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRITessellate inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), label_value=dict(argstr='%d', mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), subjects_dir=dict(), tesselate_all_voxels=dict(argstr='-a'), use_real_RAS_coordinates=dict(argstr='-n'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), label_value=dict(argstr='%d', mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), subjects_dir=dict(), tesselate_all_voxels=dict(argstr='-a'), use_real_RAS_coordinates=dict(argstr='-n'))
```

## Next Steps


---

*Source: test_auto_MRITessellate.py:6 | Complexity: Beginner | Last updated: 2026-05-18*