# How To: Curvatureanisotropicdiffusion Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CurvatureAnisotropicDiffusion inputs

## Prerequisites

**Required Modules:**
- `denoising`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), conductance=dict(argstr='--conductance %f'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), iterations=dict(argstr='--iterations %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), timeStep=dict(argstr='--timeStep %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), conductance=dict(argstr='--conductance %f'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), iterations=dict(argstr='--iterations %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), timeStep=dict(argstr='--timeStep %f'))
```

## Next Steps


---

*Source: test_auto_CurvatureAnisotropicDiffusion.py:6 | Complexity: Beginner | Last updated: 2026-05-18*