# How To: Cannysegmentationlevelsetimagefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CannySegmentationLevelSetImageFilter inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(advectionWeight=dict(argstr='--advectionWeight %f'), args=dict(argstr='%s'), cannyThreshold=dict(argstr='--cannyThreshold %f'), cannyVariance=dict(argstr='--cannyVariance %f'), environ=dict(nohash=True, usedefault=True), initialModel=dict(argstr='--initialModel %s', extensions=None), initialModelIsovalue=dict(argstr='--initialModelIsovalue %f'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maxIterations=dict(argstr='--maxIterations %d'), outputSpeedVolume=dict(argstr='--outputSpeedVolume %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(advectionWeight=dict(argstr='--advectionWeight %f'), args=dict(argstr='%s'), cannyThreshold=dict(argstr='--cannyThreshold %f'), cannyVariance=dict(argstr='--cannyVariance %f'), environ=dict(nohash=True, usedefault=True), initialModel=dict(argstr='--initialModel %s', extensions=None), initialModelIsovalue=dict(argstr='--initialModelIsovalue %f'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maxIterations=dict(argstr='--maxIterations %d'), outputSpeedVolume=dict(argstr='--outputSpeedVolume %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_CannySegmentationLevelSetImageFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*