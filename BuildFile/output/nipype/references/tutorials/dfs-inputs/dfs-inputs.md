# How To: Dfs Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Dfs inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), curvatureWeighting=dict(argstr='-w %f', usedefault=True), environ=dict(nohash=True, usedefault=True), inputShadingVolume=dict(argstr='-c %s', extensions=None), inputVolumeFile=dict(argstr='-i %s', extensions=None, mandatory=True), noNormalsFlag=dict(argstr='--nonormals'), nonZeroTessellation=dict(argstr='-nz', xor=('nonZeroTessellation', 'specialTessellation')), outputSurfaceFile=dict(argstr='-o %s', extensions=None, genfile=True), postSmoothFlag=dict(argstr='--postsmooth'), scalingPercentile=dict(argstr='-f %f'), smoothingConstant=dict(argstr='-a %f', usedefault=True), smoothingIterations=dict(argstr='-n %d', usedefault=True), specialTessellation=dict(argstr='%s', position=-1, requires=['tessellationThreshold'], xor=('nonZeroTessellation', 'specialTessellation')), tessellationThreshold=dict(argstr='%f'), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'), zeroPadFlag=dict(argstr='-z'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), curvatureWeighting=dict(argstr='-w %f', usedefault=True), environ=dict(nohash=True, usedefault=True), inputShadingVolume=dict(argstr='-c %s', extensions=None), inputVolumeFile=dict(argstr='-i %s', extensions=None, mandatory=True), noNormalsFlag=dict(argstr='--nonormals'), nonZeroTessellation=dict(argstr='-nz', xor=('nonZeroTessellation', 'specialTessellation')), outputSurfaceFile=dict(argstr='-o %s', extensions=None, genfile=True), postSmoothFlag=dict(argstr='--postsmooth'), scalingPercentile=dict(argstr='-f %f'), smoothingConstant=dict(argstr='-a %f', usedefault=True), smoothingIterations=dict(argstr='-n %d', usedefault=True), specialTessellation=dict(argstr='%s', position=-1, requires=['tessellationThreshold'], xor=('nonZeroTessellation', 'specialTessellation')), tessellationThreshold=dict(argstr='%f'), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'), zeroPadFlag=dict(argstr='-z'))
```

## Next Steps


---

*Source: test_auto_Dfs.py:6 | Complexity: Beginner | Last updated: 2026-05-18*