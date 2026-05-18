# How To: Distancemaps Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DistanceMaps inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputLabelVolume=dict(argstr='--inputLabelVolume %s', extensions=None), inputMaskVolume=dict(argstr='--inputMaskVolume %s', extensions=None), inputTissueLabel=dict(argstr='--inputTissueLabel %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputLabelVolume=dict(argstr='--inputLabelVolume %s', extensions=None), inputMaskVolume=dict(argstr='--inputMaskVolume %s', extensions=None), inputTissueLabel=dict(argstr='--inputTissueLabel %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_DistanceMaps.py:6 | Complexity: Beginner | Last updated: 2026-05-18*