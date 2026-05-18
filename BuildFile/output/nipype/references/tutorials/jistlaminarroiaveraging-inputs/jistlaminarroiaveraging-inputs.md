# How To: Jistlaminarroiaveraging Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistLaminarROIAveraging inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inIntensity=dict(argstr='--inIntensity %s', extensions=None), inMask=dict(argstr='--inMask %s', extensions=None), inROI=dict(argstr='--inROI %s', extensions=None), inROI2=dict(argstr='--inROI2 %s'), null=dict(argstr='--null %s'), outROI3=dict(argstr='--outROI3 %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inIntensity=dict(argstr='--inIntensity %s', extensions=None), inMask=dict(argstr='--inMask %s', extensions=None), inROI=dict(argstr='--inROI %s', extensions=None), inROI2=dict(argstr='--inROI2 %s'), null=dict(argstr='--null %s'), outROI3=dict(argstr='--outROI3 %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistLaminarROIAveraging.py:6 | Complexity: Beginner | Last updated: 2026-05-18*