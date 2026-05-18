# How To: Brainslandmarkinitializer Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSLandmarkInitializer inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputFixedLandmarkFilename=dict(argstr='--inputFixedLandmarkFilename %s', extensions=None), inputMovingLandmarkFilename=dict(argstr='--inputMovingLandmarkFilename %s', extensions=None), inputWeightFilename=dict(argstr='--inputWeightFilename %s', extensions=None), outputTransformFilename=dict(argstr='--outputTransformFilename %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputFixedLandmarkFilename=dict(argstr='--inputFixedLandmarkFilename %s', extensions=None), inputMovingLandmarkFilename=dict(argstr='--inputMovingLandmarkFilename %s', extensions=None), inputWeightFilename=dict(argstr='--inputWeightFilename %s', extensions=None), outputTransformFilename=dict(argstr='--outputTransformFilename %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_BRAINSLandmarkInitializer.py:6 | Complexity: Beginner | Last updated: 2026-05-18*