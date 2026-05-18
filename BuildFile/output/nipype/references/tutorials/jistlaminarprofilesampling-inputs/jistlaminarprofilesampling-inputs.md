# How To: Jistlaminarprofilesampling Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistLaminarProfileSampling inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inCortex=dict(argstr='--inCortex %s', extensions=None), inIntensity=dict(argstr='--inIntensity %s', extensions=None), inProfile=dict(argstr='--inProfile %s', extensions=None), null=dict(argstr='--null %s'), outProfile2=dict(argstr='--outProfile2 %s', hash_files=False), outProfilemapped=dict(argstr='--outProfilemapped %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inCortex=dict(argstr='--inCortex %s', extensions=None), inIntensity=dict(argstr='--inIntensity %s', extensions=None), inProfile=dict(argstr='--inProfile %s', extensions=None), null=dict(argstr='--null %s'), outProfile2=dict(argstr='--outProfile2 %s', hash_files=False), outProfilemapped=dict(argstr='--outProfilemapped %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistLaminarProfileSampling.py:6 | Complexity: Beginner | Last updated: 2026-05-18*