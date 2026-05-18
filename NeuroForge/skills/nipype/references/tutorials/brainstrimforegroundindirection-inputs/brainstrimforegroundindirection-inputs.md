# How To: Brainstrimforegroundindirection Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSTrimForegroundInDirection inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(BackgroundFillValue=dict(argstr='--BackgroundFillValue %s'), args=dict(argstr='%s'), closingSize=dict(argstr='--closingSize %d'), directionCode=dict(argstr='--directionCode %d'), environ=dict(nohash=True, usedefault=True), headSizeLimit=dict(argstr='--headSizeLimit %f'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), otsuPercentileThreshold=dict(argstr='--otsuPercentileThreshold %f'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(BackgroundFillValue=dict(argstr='--BackgroundFillValue %s'), args=dict(argstr='%s'), closingSize=dict(argstr='--closingSize %d'), directionCode=dict(argstr='--directionCode %d'), environ=dict(nohash=True, usedefault=True), headSizeLimit=dict(argstr='--headSizeLimit %f'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), otsuPercentileThreshold=dict(argstr='--otsuPercentileThreshold %f'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_BRAINSTrimForegroundInDirection.py:6 | Complexity: Beginner | Last updated: 2026-05-18*