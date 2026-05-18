# How To: Neighborhoodmedian Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NeighborhoodMedian inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputMaskVolume=dict(argstr='--inputMaskVolume %s', extensions=None), inputRadius=dict(argstr='--inputRadius %d'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputMaskVolume=dict(argstr='--inputMaskVolume %s', extensions=None), inputRadius=dict(argstr='--inputRadius %d'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_NeighborhoodMedian.py:6 | Complexity: Beginner | Last updated: 2026-05-18*