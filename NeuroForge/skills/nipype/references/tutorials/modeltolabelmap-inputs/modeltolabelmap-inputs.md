# How To: Modeltolabelmap Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ModelToLabelMap inputs

## Prerequisites

**Required Modules:**
- `surface`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-3), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), distance=dict(argstr='--distance %f'), environ=dict(nohash=True, usedefault=True), surface=dict(argstr='%s', extensions=None, position=-2))
```


## Complete Example

```python
# Workflow
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-3), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), distance=dict(argstr='--distance %f'), environ=dict(nohash=True, usedefault=True), surface=dict(argstr='%s', extensions=None, position=-2))
```

## Next Steps


---

*Source: test_auto_ModelToLabelMap.py:6 | Complexity: Beginner | Last updated: 2026-05-18*