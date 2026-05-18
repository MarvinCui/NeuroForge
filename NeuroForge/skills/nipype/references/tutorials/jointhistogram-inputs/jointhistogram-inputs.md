# How To: Jointhistogram Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JointHistogram inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputMaskVolumeInXAxis=dict(argstr='--inputMaskVolumeInXAxis %s', extensions=None), inputMaskVolumeInYAxis=dict(argstr='--inputMaskVolumeInYAxis %s', extensions=None), inputVolumeInXAxis=dict(argstr='--inputVolumeInXAxis %s', extensions=None), inputVolumeInYAxis=dict(argstr='--inputVolumeInYAxis %s', extensions=None), outputJointHistogramImage=dict(argstr='--outputJointHistogramImage %s'), verbose=dict(argstr='--verbose '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputMaskVolumeInXAxis=dict(argstr='--inputMaskVolumeInXAxis %s', extensions=None), inputMaskVolumeInYAxis=dict(argstr='--inputMaskVolumeInYAxis %s', extensions=None), inputVolumeInXAxis=dict(argstr='--inputVolumeInXAxis %s', extensions=None), inputVolumeInYAxis=dict(argstr='--inputVolumeInYAxis %s', extensions=None), outputJointHistogramImage=dict(argstr='--outputJointHistogramImage %s'), verbose=dict(argstr='--verbose '))
```

## Next Steps


---

*Source: test_auto_JointHistogram.py:6 | Complexity: Beginner | Last updated: 2026-05-18*