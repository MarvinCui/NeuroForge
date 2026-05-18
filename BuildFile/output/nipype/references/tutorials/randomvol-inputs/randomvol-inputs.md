# How To: Randomvol Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RandomVol inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inField=dict(argstr='--inField %s'), inLambda=dict(argstr='--inLambda %f'), inMaximum=dict(argstr='--inMaximum %d'), inMinimum=dict(argstr='--inMinimum %d'), inSize=dict(argstr='--inSize %d'), inSize2=dict(argstr='--inSize2 %d'), inSize3=dict(argstr='--inSize3 %d'), inSize4=dict(argstr='--inSize4 %d'), inStandard=dict(argstr='--inStandard %d'), null=dict(argstr='--null %s'), outRand1=dict(argstr='--outRand1 %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inField=dict(argstr='--inField %s'), inLambda=dict(argstr='--inLambda %f'), inMaximum=dict(argstr='--inMaximum %d'), inMinimum=dict(argstr='--inMinimum %d'), inSize=dict(argstr='--inSize %d'), inSize2=dict(argstr='--inSize2 %d'), inSize3=dict(argstr='--inSize3 %d'), inSize4=dict(argstr='--inSize4 %d'), inStandard=dict(argstr='--inStandard %d'), null=dict(argstr='--null %s'), outRand1=dict(argstr='--outRand1 %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_RandomVol.py:6 | Complexity: Beginner | Last updated: 2026-05-18*