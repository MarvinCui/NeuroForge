# How To: Mrimarchingcubes Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRIMarchingCubes inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), connectivity_value=dict(argstr='%d', position=-1, usedefault=True), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), label_value=dict(argstr='%d', mandatory=True, position=2), out_file=dict(argstr='./%s', extensions=None, genfile=True, position=-2), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), connectivity_value=dict(argstr='%d', position=-1, usedefault=True), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), label_value=dict(argstr='%d', mandatory=True, position=2), out_file=dict(argstr='./%s', extensions=None, genfile=True, position=-2), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_MRIMarchingCubes.py:6 | Complexity: Beginner | Last updated: 2026-05-18*