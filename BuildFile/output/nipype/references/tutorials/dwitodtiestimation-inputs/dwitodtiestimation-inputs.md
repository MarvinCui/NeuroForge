# How To: Dwitodtiestimation Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIToDTIEstimation inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), enumeration=dict(argstr='--enumeration %s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-3), mask=dict(argstr='--mask %s', extensions=None), outputBaseline=dict(argstr='%s', hash_files=False, position=-1), outputTensor=dict(argstr='%s', hash_files=False, position=-2), shiftNeg=dict(argstr='--shiftNeg '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), enumeration=dict(argstr='--enumeration %s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-3), mask=dict(argstr='--mask %s', extensions=None), outputBaseline=dict(argstr='%s', hash_files=False, position=-1), outputTensor=dict(argstr='%s', hash_files=False, position=-2), shiftNeg=dict(argstr='--shiftNeg '))
```

## Next Steps


---

*Source: test_auto_DWIToDTIEstimation.py:6 | Complexity: Beginner | Last updated: 2026-05-18*