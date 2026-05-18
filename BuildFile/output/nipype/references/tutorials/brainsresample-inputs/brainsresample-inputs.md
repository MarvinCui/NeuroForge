# How To: Brainsresample Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSResample inputs

## Prerequisites

**Required Modules:**
- `brainsresample`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), defaultValue=dict(argstr='--defaultValue %f'), deformationVolume=dict(argstr='--deformationVolume %s', extensions=None), environ=dict(nohash=True, usedefault=True), gridSpacing=dict(argstr='--gridSpacing %s', sep=','), inputVolume=dict(argstr='--inputVolume %s', extensions=None), interpolationMode=dict(argstr='--interpolationMode %s'), inverseTransform=dict(argstr='--inverseTransform '), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), pixelType=dict(argstr='--pixelType %s'), referenceVolume=dict(argstr='--referenceVolume %s', extensions=None), warpTransform=dict(argstr='--warpTransform %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), defaultValue=dict(argstr='--defaultValue %f'), deformationVolume=dict(argstr='--deformationVolume %s', extensions=None), environ=dict(nohash=True, usedefault=True), gridSpacing=dict(argstr='--gridSpacing %s', sep=','), inputVolume=dict(argstr='--inputVolume %s', extensions=None), interpolationMode=dict(argstr='--interpolationMode %s'), inverseTransform=dict(argstr='--inverseTransform '), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), pixelType=dict(argstr='--pixelType %s'), referenceVolume=dict(argstr='--referenceVolume %s', extensions=None), warpTransform=dict(argstr='--warpTransform %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_BRAINSResample.py:6 | Complexity: Beginner | Last updated: 2026-05-18*