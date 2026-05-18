# How To: Maskscalarvolume Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MaskScalarVolume inputs

## Prerequisites

**Required Modules:**
- `arithmetic`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-3), MaskVolume=dict(argstr='%s', extensions=None, position=-2), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), label=dict(argstr='--label %d'), replace=dict(argstr='--replace %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-3), MaskVolume=dict(argstr='%s', extensions=None, position=-2), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), label=dict(argstr='--label %d'), replace=dict(argstr='--replace %d'))
```

## Next Steps


---

*Source: test_auto_MaskScalarVolume.py:6 | Complexity: Beginner | Last updated: 2026-05-18*