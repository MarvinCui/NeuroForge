# How To: Castscalarvolume Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CastScalarVolume inputs

## Prerequisites

**Required Modules:**
- `arithmetic`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), type=dict(argstr='--type %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), type=dict(argstr='--type %s'))
```

## Next Steps


---

*Source: test_auto_CastScalarVolume.py:6 | Complexity: Beginner | Last updated: 2026-05-18*