# How To: Pialmesh Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Pialmesh inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), exportPrefix=dict(argstr='--prefix %s'), inputMaskFile=dict(argstr='-m %s', extensions=None, mandatory=True), inputSurfaceFile=dict(argstr='-i %s', extensions=None, mandatory=True), inputTissueFractionFile=dict(argstr='-f %s', extensions=None, mandatory=True), laplacianSmoothing=dict(argstr='--smooth %f', usedefault=True), maxThickness=dict(argstr='--max %f', usedefault=True), normalSmoother=dict(argstr='--nc %f', usedefault=True), numIterations=dict(argstr='-n %d', usedefault=True), outputInterval=dict(argstr='--interval %d', usedefault=True), outputSurfaceFile=dict(argstr='-o %s', extensions=None, genfile=True), recomputeNormals=dict(argstr='--norm'), searchRadius=dict(argstr='-r %f', usedefault=True), stepSize=dict(argstr='-s %f', usedefault=True), tangentSmoother=dict(argstr='--tc %f'), timer=dict(argstr='--timer'), tissueThreshold=dict(argstr='-t %f', usedefault=True), verbosity=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), exportPrefix=dict(argstr='--prefix %s'), inputMaskFile=dict(argstr='-m %s', extensions=None, mandatory=True), inputSurfaceFile=dict(argstr='-i %s', extensions=None, mandatory=True), inputTissueFractionFile=dict(argstr='-f %s', extensions=None, mandatory=True), laplacianSmoothing=dict(argstr='--smooth %f', usedefault=True), maxThickness=dict(argstr='--max %f', usedefault=True), normalSmoother=dict(argstr='--nc %f', usedefault=True), numIterations=dict(argstr='-n %d', usedefault=True), outputInterval=dict(argstr='--interval %d', usedefault=True), outputSurfaceFile=dict(argstr='-o %s', extensions=None, genfile=True), recomputeNormals=dict(argstr='--norm'), searchRadius=dict(argstr='-r %f', usedefault=True), stepSize=dict(argstr='-s %f', usedefault=True), tangentSmoother=dict(argstr='--tc %f'), timer=dict(argstr='--timer'), tissueThreshold=dict(argstr='-t %f', usedefault=True), verbosity=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Pialmesh.py:6 | Complexity: Beginner | Last updated: 2026-05-18*