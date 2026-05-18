# How To: Dilatemask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DilateMask inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputBinaryVolume=dict(argstr='--inputBinaryVolume %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), lowerThreshold=dict(argstr='--lowerThreshold %f'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), sizeStructuralElement=dict(argstr='--sizeStructuralElement %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputBinaryVolume=dict(argstr='--inputBinaryVolume %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), lowerThreshold=dict(argstr='--lowerThreshold %f'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), sizeStructuralElement=dict(argstr='--sizeStructuralElement %d'))
```

## Next Steps


---

*Source: test_auto_DilateMask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*