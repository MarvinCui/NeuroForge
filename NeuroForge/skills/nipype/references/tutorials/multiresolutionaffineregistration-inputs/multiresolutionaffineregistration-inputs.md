# How To: Multiresolutionaffineregistration Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MultiResolutionAffineRegistration inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixedImage=dict(argstr='%s', extensions=None, position=-2), fixedImageMask=dict(argstr='--fixedImageMask %s', extensions=None), fixedImageROI=dict(argstr='--fixedImageROI %s'), metricTolerance=dict(argstr='--metricTolerance %f'), movingImage=dict(argstr='%s', extensions=None, position=-1), numIterations=dict(argstr='--numIterations %d'), numLineIterations=dict(argstr='--numLineIterations %d'), resampledImage=dict(argstr='--resampledImage %s', hash_files=False), saveTransform=dict(argstr='--saveTransform %s', hash_files=False), stepSize=dict(argstr='--stepSize %f'), stepTolerance=dict(argstr='--stepTolerance %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixedImage=dict(argstr='%s', extensions=None, position=-2), fixedImageMask=dict(argstr='--fixedImageMask %s', extensions=None), fixedImageROI=dict(argstr='--fixedImageROI %s'), metricTolerance=dict(argstr='--metricTolerance %f'), movingImage=dict(argstr='%s', extensions=None, position=-1), numIterations=dict(argstr='--numIterations %d'), numLineIterations=dict(argstr='--numLineIterations %d'), resampledImage=dict(argstr='--resampledImage %s', hash_files=False), saveTransform=dict(argstr='--saveTransform %s', hash_files=False), stepSize=dict(argstr='--stepSize %f'), stepTolerance=dict(argstr='--stepTolerance %f'))
```

## Next Steps


---

*Source: test_auto_MultiResolutionAffineRegistration.py:6 | Complexity: Beginner | Last updated: 2026-05-18*