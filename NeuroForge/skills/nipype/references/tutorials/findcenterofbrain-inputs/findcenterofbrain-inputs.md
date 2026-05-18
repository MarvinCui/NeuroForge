# How To: Findcenterofbrain Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FindCenterOfBrain inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), axis=dict(argstr='--axis %d'), backgroundValue=dict(argstr='--backgroundValue %d'), clippedImageMask=dict(argstr='--clippedImageMask %s', hash_files=False), closingSize=dict(argstr='--closingSize %d'), debugAfterGridComputationsForegroundImage=dict(argstr='--debugAfterGridComputationsForegroundImage %s', hash_files=False), debugClippedImageMask=dict(argstr='--debugClippedImageMask %s', hash_files=False), debugDistanceImage=dict(argstr='--debugDistanceImage %s', hash_files=False), debugGridImage=dict(argstr='--debugGridImage %s', hash_files=False), debugTrimmedImage=dict(argstr='--debugTrimmedImage %s', hash_files=False), environ=dict(nohash=True, usedefault=True), generateDebugImages=dict(argstr='--generateDebugImages '), headSizeEstimate=dict(argstr='--headSizeEstimate %f'), headSizeLimit=dict(argstr='--headSizeLimit %f'), imageMask=dict(argstr='--imageMask %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maximize=dict(argstr='--maximize '), otsuPercentileThreshold=dict(argstr='--otsuPercentileThreshold %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), axis=dict(argstr='--axis %d'), backgroundValue=dict(argstr='--backgroundValue %d'), clippedImageMask=dict(argstr='--clippedImageMask %s', hash_files=False), closingSize=dict(argstr='--closingSize %d'), debugAfterGridComputationsForegroundImage=dict(argstr='--debugAfterGridComputationsForegroundImage %s', hash_files=False), debugClippedImageMask=dict(argstr='--debugClippedImageMask %s', hash_files=False), debugDistanceImage=dict(argstr='--debugDistanceImage %s', hash_files=False), debugGridImage=dict(argstr='--debugGridImage %s', hash_files=False), debugTrimmedImage=dict(argstr='--debugTrimmedImage %s', hash_files=False), environ=dict(nohash=True, usedefault=True), generateDebugImages=dict(argstr='--generateDebugImages '), headSizeEstimate=dict(argstr='--headSizeEstimate %f'), headSizeLimit=dict(argstr='--headSizeLimit %f'), imageMask=dict(argstr='--imageMask %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maximize=dict(argstr='--maximize '), otsuPercentileThreshold=dict(argstr='--otsuPercentileThreshold %f'))
```

## Next Steps


---

*Source: test_auto_FindCenterOfBrain.py:6 | Complexity: Beginner | Last updated: 2026-05-18*