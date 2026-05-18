# How To: Jistlaminarprofilecalculator Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistLaminarProfileCalculator inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inIntensity=dict(argstr='--inIntensity %s', extensions=None), inMask=dict(argstr='--inMask %s', extensions=None), incomputed=dict(argstr='--incomputed %s'), null=dict(argstr='--null %s'), outResult=dict(argstr='--outResult %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inIntensity=dict(argstr='--inIntensity %s', extensions=None), inMask=dict(argstr='--inMask %s', extensions=None), incomputed=dict(argstr='--incomputed %s'), null=dict(argstr='--null %s'), outResult=dict(argstr='--outResult %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistLaminarProfileCalculator.py:6 | Complexity: Beginner | Last updated: 2026-05-18*