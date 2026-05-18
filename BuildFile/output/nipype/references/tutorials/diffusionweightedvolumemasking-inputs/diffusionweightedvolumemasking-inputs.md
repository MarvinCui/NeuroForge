# How To: Diffusionweightedvolumemasking Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DiffusionWeightedVolumeMasking inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-4), otsuomegathreshold=dict(argstr='--otsuomegathreshold %f'), outputBaseline=dict(argstr='%s', hash_files=False, position=-2), removeislands=dict(argstr='--removeislands '), thresholdMask=dict(argstr='%s', hash_files=False, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-4), otsuomegathreshold=dict(argstr='--otsuomegathreshold %f'), outputBaseline=dict(argstr='%s', hash_files=False, position=-2), removeislands=dict(argstr='--removeislands '), thresholdMask=dict(argstr='%s', hash_files=False, position=-1))
```

## Next Steps


---

*Source: test_auto_DiffusionWeightedVolumeMasking.py:6 | Complexity: Beginner | Last updated: 2026-05-18*