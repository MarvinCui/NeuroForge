# How To: Medicalgorithmn3 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MedicAlgorithmN3 inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inAutomatic=dict(argstr='--inAutomatic %s'), inEnd=dict(argstr='--inEnd %f'), inField=dict(argstr='--inField %f'), inInput=dict(argstr='--inInput %s', extensions=None), inKernel=dict(argstr='--inKernel %f'), inMaximum=dict(argstr='--inMaximum %d'), inSignal=dict(argstr='--inSignal %f'), inSubsample=dict(argstr='--inSubsample %f'), inWeiner=dict(argstr='--inWeiner %f'), null=dict(argstr='--null %s'), outInhomogeneity=dict(argstr='--outInhomogeneity %s', hash_files=False), outInhomogeneity2=dict(argstr='--outInhomogeneity2 %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inAutomatic=dict(argstr='--inAutomatic %s'), inEnd=dict(argstr='--inEnd %f'), inField=dict(argstr='--inField %f'), inInput=dict(argstr='--inInput %s', extensions=None), inKernel=dict(argstr='--inKernel %f'), inMaximum=dict(argstr='--inMaximum %d'), inSignal=dict(argstr='--inSignal %f'), inSubsample=dict(argstr='--inSubsample %f'), inWeiner=dict(argstr='--inWeiner %f'), null=dict(argstr='--null %s'), outInhomogeneity=dict(argstr='--outInhomogeneity %s', hash_files=False), outInhomogeneity2=dict(argstr='--outInhomogeneity2 %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_MedicAlgorithmN3.py:6 | Complexity: Beginner | Last updated: 2026-05-18*