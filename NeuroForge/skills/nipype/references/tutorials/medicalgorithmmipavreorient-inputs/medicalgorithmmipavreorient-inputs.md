# How To: Medicalgorithmmipavreorient Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MedicAlgorithmMipavReorient inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inInterpolation=dict(argstr='--inInterpolation %s'), inNew=dict(argstr='--inNew %s'), inResolution=dict(argstr='--inResolution %s'), inSource=dict(argstr='--inSource %s', sep=';'), inTemplate=dict(argstr='--inTemplate %s', extensions=None), inUser=dict(argstr='--inUser %s'), inUser2=dict(argstr='--inUser2 %s'), inUser3=dict(argstr='--inUser3 %s'), inUser4=dict(argstr='--inUser4 %s'), null=dict(argstr='--null %s'), outReoriented=dict(argstr='--outReoriented %s', sep=';'), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inInterpolation=dict(argstr='--inInterpolation %s'), inNew=dict(argstr='--inNew %s'), inResolution=dict(argstr='--inResolution %s'), inSource=dict(argstr='--inSource %s', sep=';'), inTemplate=dict(argstr='--inTemplate %s', extensions=None), inUser=dict(argstr='--inUser %s'), inUser2=dict(argstr='--inUser2 %s'), inUser3=dict(argstr='--inUser3 %s'), inUser4=dict(argstr='--inUser4 %s'), null=dict(argstr='--null %s'), outReoriented=dict(argstr='--outReoriented %s', sep=';'), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_MedicAlgorithmMipavReorient.py:6 | Complexity: Beginner | Last updated: 2026-05-18*