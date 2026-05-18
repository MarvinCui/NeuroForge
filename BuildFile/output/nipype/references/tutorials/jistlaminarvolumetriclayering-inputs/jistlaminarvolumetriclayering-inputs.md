# How To: Jistlaminarvolumetriclayering Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistLaminarVolumetricLayering inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inInner=dict(argstr='--inInner %s', extensions=None), inLayering=dict(argstr='--inLayering %s'), inLayering2=dict(argstr='--inLayering2 %s'), inMax=dict(argstr='--inMax %d'), inMin=dict(argstr='--inMin %f'), inNumber=dict(argstr='--inNumber %d'), inOuter=dict(argstr='--inOuter %s', extensions=None), inTopology=dict(argstr='--inTopology %s'), incurvature=dict(argstr='--incurvature %d'), inpresmooth=dict(argstr='--inpresmooth %s'), inratio=dict(argstr='--inratio %f'), null=dict(argstr='--null %s'), outContinuous=dict(argstr='--outContinuous %s', hash_files=False), outDiscrete=dict(argstr='--outDiscrete %s', hash_files=False), outLayer=dict(argstr='--outLayer %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inInner=dict(argstr='--inInner %s', extensions=None), inLayering=dict(argstr='--inLayering %s'), inLayering2=dict(argstr='--inLayering2 %s'), inMax=dict(argstr='--inMax %d'), inMin=dict(argstr='--inMin %f'), inNumber=dict(argstr='--inNumber %d'), inOuter=dict(argstr='--inOuter %s', extensions=None), inTopology=dict(argstr='--inTopology %s'), incurvature=dict(argstr='--incurvature %d'), inpresmooth=dict(argstr='--inpresmooth %s'), inratio=dict(argstr='--inratio %f'), null=dict(argstr='--null %s'), outContinuous=dict(argstr='--outContinuous %s', hash_files=False), outDiscrete=dict(argstr='--outDiscrete %s', hash_files=False), outLayer=dict(argstr='--outLayer %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistLaminarVolumetricLayering.py:6 | Complexity: Beginner | Last updated: 2026-05-18*