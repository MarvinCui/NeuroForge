# How To: Imagelabelcombine Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ImageLabelCombine inputs

## Prerequisites

**Required Modules:**
- `imagelabelcombine`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputLabelMap_A=dict(argstr='%s', extensions=None, position=-3), InputLabelMap_B=dict(argstr='%s', extensions=None, position=-2), OutputLabelMap=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), first_overwrites=dict(argstr='--first_overwrites '))
```


## Complete Example

```python
# Workflow
input_map = dict(InputLabelMap_A=dict(argstr='%s', extensions=None, position=-3), InputLabelMap_B=dict(argstr='%s', extensions=None, position=-2), OutputLabelMap=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), first_overwrites=dict(argstr='--first_overwrites '))
```

## Next Steps


---

*Source: test_auto_ImageLabelCombine.py:6 | Complexity: Beginner | Last updated: 2026-05-18*