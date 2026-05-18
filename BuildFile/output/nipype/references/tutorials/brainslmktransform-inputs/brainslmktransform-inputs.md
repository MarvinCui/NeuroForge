# How To: Brainslmktransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSLmkTransform inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputFixedLandmarks=dict(argstr='--inputFixedLandmarks %s', extensions=None), inputMovingLandmarks=dict(argstr='--inputMovingLandmarks %s', extensions=None), inputMovingVolume=dict(argstr='--inputMovingVolume %s', extensions=None), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputAffineTransform=dict(argstr='--outputAffineTransform %s', hash_files=False), outputResampledVolume=dict(argstr='--outputResampledVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputFixedLandmarks=dict(argstr='--inputFixedLandmarks %s', extensions=None), inputMovingLandmarks=dict(argstr='--inputMovingLandmarks %s', extensions=None), inputMovingVolume=dict(argstr='--inputMovingVolume %s', extensions=None), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputAffineTransform=dict(argstr='--outputAffineTransform %s', hash_files=False), outputResampledVolume=dict(argstr='--outputResampledVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_BRAINSLmkTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*