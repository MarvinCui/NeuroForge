# How To: Brainsinitializedcontrolpoints Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSInitializedControlPoints inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputLandmarksFile=dict(argstr='--outputLandmarksFile %s'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), permuteOrder=dict(argstr='--permuteOrder %s', sep=','), splineGridSize=dict(argstr='--splineGridSize %s', sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputLandmarksFile=dict(argstr='--outputLandmarksFile %s'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), permuteOrder=dict(argstr='--permuteOrder %s', sep=','), splineGridSize=dict(argstr='--splineGridSize %s', sep=','))
```

## Next Steps


---

*Source: test_auto_BRAINSInitializedControlPoints.py:6 | Complexity: Beginner | Last updated: 2026-05-18*