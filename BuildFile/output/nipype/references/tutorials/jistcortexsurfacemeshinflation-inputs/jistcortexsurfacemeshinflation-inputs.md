# How To: Jistcortexsurfacemeshinflation Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistCortexSurfaceMeshInflation inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inLevelset=dict(argstr='--inLevelset %s', extensions=None), inLorentzian=dict(argstr='--inLorentzian %s'), inMax=dict(argstr='--inMax %d'), inMean=dict(argstr='--inMean %f'), inSOR=dict(argstr='--inSOR %f'), inStep=dict(argstr='--inStep %d'), inTopology=dict(argstr='--inTopology %s'), null=dict(argstr='--null %s'), outInflated=dict(argstr='--outInflated %s', hash_files=False), outOriginal=dict(argstr='--outOriginal %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inLevelset=dict(argstr='--inLevelset %s', extensions=None), inLorentzian=dict(argstr='--inLorentzian %s'), inMax=dict(argstr='--inMax %d'), inMean=dict(argstr='--inMean %f'), inSOR=dict(argstr='--inSOR %f'), inStep=dict(argstr='--inStep %d'), inTopology=dict(argstr='--inTopology %s'), null=dict(argstr='--null %s'), outInflated=dict(argstr='--outInflated %s', hash_files=False), outOriginal=dict(argstr='--outOriginal %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistCortexSurfaceMeshInflation.py:6 | Complexity: Beginner | Last updated: 2026-05-18*