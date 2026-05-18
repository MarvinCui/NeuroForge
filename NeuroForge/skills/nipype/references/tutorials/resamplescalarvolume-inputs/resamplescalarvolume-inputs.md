# How To: Resamplescalarvolume Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ResampleScalarVolume inputs

## Prerequisites

**Required Modules:**
- `filtering`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), interpolation=dict(argstr='--interpolation %s'), spacing=dict(argstr='--spacing %s', sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), interpolation=dict(argstr='--interpolation %s'), spacing=dict(argstr='--spacing %s', sep=','))
```

## Next Steps


---

*Source: test_auto_ResampleScalarVolume.py:6 | Complexity: Beginner | Last updated: 2026-05-18*