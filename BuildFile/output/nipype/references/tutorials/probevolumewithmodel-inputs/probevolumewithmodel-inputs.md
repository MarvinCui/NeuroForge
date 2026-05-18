# How To: Probevolumewithmodel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ProbeVolumeWithModel inputs

## Prerequisites

**Required Modules:**
- `surface`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputModel=dict(argstr='%s', extensions=None, position=-2), InputVolume=dict(argstr='%s', extensions=None, position=-3), OutputModel=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(InputModel=dict(argstr='%s', extensions=None, position=-2), InputVolume=dict(argstr='%s', extensions=None, position=-3), OutputModel=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True))
```

## Next Steps


---

*Source: test_auto_ProbeVolumeWithModel.py:6 | Complexity: Beginner | Last updated: 2026-05-18*