# How To: Gradientanisotropicdiffusionimagefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GradientAnisotropicDiffusionImageFilter inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), conductance=dict(argstr='--conductance %f'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfIterations=dict(argstr='--numberOfIterations %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), timeStep=dict(argstr='--timeStep %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), conductance=dict(argstr='--conductance %f'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfIterations=dict(argstr='--numberOfIterations %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), timeStep=dict(argstr='--timeStep %f'))
```

## Next Steps


---

*Source: test_auto_GradientAnisotropicDiffusionImageFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*