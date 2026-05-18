# How To: Medicalgorithmthresholdtobinarymask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MedicAlgorithmThresholdToBinaryMask inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inLabel=dict(argstr='--inLabel %s', sep=';'), inMaximum=dict(argstr='--inMaximum %f'), inMinimum=dict(argstr='--inMinimum %f'), inUse=dict(argstr='--inUse %s'), null=dict(argstr='--null %s'), outBinary=dict(argstr='--outBinary %s', sep=';'), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inLabel=dict(argstr='--inLabel %s', sep=';'), inMaximum=dict(argstr='--inMaximum %f'), inMinimum=dict(argstr='--inMinimum %f'), inUse=dict(argstr='--inUse %s'), null=dict(argstr='--null %s'), outBinary=dict(argstr='--outBinary %s', sep=';'), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_MedicAlgorithmThresholdToBinaryMask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*