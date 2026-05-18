# How To: Labelmapsmoothing Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test LabelMapSmoothing inputs

## Prerequisites

**Required Modules:**
- `surface`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), gaussianSigma=dict(argstr='--gaussianSigma %f'), inputVolume=dict(argstr='%s', extensions=None, position=-2), labelToSmooth=dict(argstr='--labelToSmooth %d'), maxRMSError=dict(argstr='--maxRMSError %f'), numberOfIterations=dict(argstr='--numberOfIterations %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), gaussianSigma=dict(argstr='--gaussianSigma %f'), inputVolume=dict(argstr='%s', extensions=None, position=-2), labelToSmooth=dict(argstr='--labelToSmooth %d'), maxRMSError=dict(argstr='--maxRMSError %f'), numberOfIterations=dict(argstr='--numberOfIterations %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```

## Next Steps


---

*Source: test_auto_LabelMapSmoothing.py:6 | Complexity: Beginner | Last updated: 2026-05-18*