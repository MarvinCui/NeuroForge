# How To: Image2Voxel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Image2Voxel inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-4dimage %s', extensions=None, mandatory=True, position=1), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), out_type=dict(argstr='-outputdatatype %s', position=2, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-4dimage %s', extensions=None, mandatory=True, position=1), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), out_type=dict(argstr='-outputdatatype %s', position=2, usedefault=True))
```

## Next Steps


---

*Source: test_auto_Image2Voxel.py:6 | Complexity: Beginner | Last updated: 2026-05-18*