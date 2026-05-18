# How To: Bsplinedeformableregistration Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BSplineDeformableRegistration inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(FixedImageFileName=dict(argstr='%s', extensions=None, position=-2), MovingImageFileName=dict(argstr='%s', extensions=None, position=-1), args=dict(argstr='%s'), constrain=dict(argstr='--constrain '), default=dict(argstr='--default %d'), environ=dict(nohash=True, usedefault=True), gridSize=dict(argstr='--gridSize %d'), histogrambins=dict(argstr='--histogrambins %d'), initialtransform=dict(argstr='--initialtransform %s', extensions=None), iterations=dict(argstr='--iterations %d'), maximumDeformation=dict(argstr='--maximumDeformation %f'), outputtransform=dict(argstr='--outputtransform %s', hash_files=False), outputwarp=dict(argstr='--outputwarp %s', hash_files=False), resampledmovingfilename=dict(argstr='--resampledmovingfilename %s', hash_files=False), spatialsamples=dict(argstr='--spatialsamples %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(FixedImageFileName=dict(argstr='%s', extensions=None, position=-2), MovingImageFileName=dict(argstr='%s', extensions=None, position=-1), args=dict(argstr='%s'), constrain=dict(argstr='--constrain '), default=dict(argstr='--default %d'), environ=dict(nohash=True, usedefault=True), gridSize=dict(argstr='--gridSize %d'), histogrambins=dict(argstr='--histogrambins %d'), initialtransform=dict(argstr='--initialtransform %s', extensions=None), iterations=dict(argstr='--iterations %d'), maximumDeformation=dict(argstr='--maximumDeformation %f'), outputtransform=dict(argstr='--outputtransform %s', hash_files=False), outputwarp=dict(argstr='--outputwarp %s', hash_files=False), resampledmovingfilename=dict(argstr='--resampledmovingfilename %s', hash_files=False), spatialsamples=dict(argstr='--spatialsamples %d'))
```

## Next Steps


---

*Source: test_auto_BSplineDeformableRegistration.py:6 | Complexity: Beginner | Last updated: 2026-05-18*