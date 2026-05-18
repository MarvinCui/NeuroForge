# How To: Affineregistration Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AffineRegistration inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(FixedImageFileName=dict(argstr='%s', extensions=None, position=-2), MovingImageFileName=dict(argstr='%s', extensions=None, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixedsmoothingfactor=dict(argstr='--fixedsmoothingfactor %d'), histogrambins=dict(argstr='--histogrambins %d'), initialtransform=dict(argstr='--initialtransform %s', extensions=None), iterations=dict(argstr='--iterations %d'), movingsmoothingfactor=dict(argstr='--movingsmoothingfactor %d'), outputtransform=dict(argstr='--outputtransform %s', hash_files=False), resampledmovingfilename=dict(argstr='--resampledmovingfilename %s', hash_files=False), spatialsamples=dict(argstr='--spatialsamples %d'), translationscale=dict(argstr='--translationscale %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(FixedImageFileName=dict(argstr='%s', extensions=None, position=-2), MovingImageFileName=dict(argstr='%s', extensions=None, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixedsmoothingfactor=dict(argstr='--fixedsmoothingfactor %d'), histogrambins=dict(argstr='--histogrambins %d'), initialtransform=dict(argstr='--initialtransform %s', extensions=None), iterations=dict(argstr='--iterations %d'), movingsmoothingfactor=dict(argstr='--movingsmoothingfactor %d'), outputtransform=dict(argstr='--outputtransform %s', hash_files=False), resampledmovingfilename=dict(argstr='--resampledmovingfilename %s', hash_files=False), spatialsamples=dict(argstr='--spatialsamples %d'), translationscale=dict(argstr='--translationscale %f'))
```

## Next Steps


---

*Source: test_auto_AffineRegistration.py:6 | Complexity: Beginner | Last updated: 2026-05-18*