# How To: Gtractinvertbsplinetransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractInvertBSplineTransform inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), inputTransform=dict(argstr='--inputTransform %s', extensions=None), landmarkDensity=dict(argstr='--landmarkDensity %s', sep=','), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTransform=dict(argstr='--outputTransform %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), inputTransform=dict(argstr='--inputTransform %s', extensions=None), landmarkDensity=dict(argstr='--landmarkDensity %s', sep=','), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTransform=dict(argstr='--outputTransform %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_gtractInvertBSplineTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*