# How To: Brainsclipinferior Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSClipInferior inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(BackgroundFillValue=dict(argstr='--BackgroundFillValue %s'), acLowerBound=dict(argstr='--acLowerBound %f'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(BackgroundFillValue=dict(argstr='--BackgroundFillValue %s'), acLowerBound=dict(argstr='--acLowerBound %f'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_BRAINSClipInferior.py:6 | Complexity: Beginner | Last updated: 2026-05-18*