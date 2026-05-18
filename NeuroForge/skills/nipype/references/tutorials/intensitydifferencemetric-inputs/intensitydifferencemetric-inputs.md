# How To: Intensitydifferencemetric Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test IntensityDifferenceMetric inputs

## Prerequisites

**Required Modules:**
- `changequantification`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), baselineSegmentationVolume=dict(argstr='%s', extensions=None, position=-3), baselineVolume=dict(argstr='%s', extensions=None, position=-4), changingBandSize=dict(argstr='--changingBandSize %d'), environ=dict(nohash=True, usedefault=True), followupVolume=dict(argstr='%s', extensions=None, position=-2), outputVolume=dict(argstr='%s', hash_files=False, position=-1), reportFileName=dict(argstr='--reportFileName %s', hash_files=False), sensitivityThreshold=dict(argstr='--sensitivityThreshold %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), baselineSegmentationVolume=dict(argstr='%s', extensions=None, position=-3), baselineVolume=dict(argstr='%s', extensions=None, position=-4), changingBandSize=dict(argstr='--changingBandSize %d'), environ=dict(nohash=True, usedefault=True), followupVolume=dict(argstr='%s', extensions=None, position=-2), outputVolume=dict(argstr='%s', hash_files=False, position=-1), reportFileName=dict(argstr='--reportFileName %s', hash_files=False), sensitivityThreshold=dict(argstr='--sensitivityThreshold %f'))
```

## Next Steps


---

*Source: test_auto_IntensityDifferenceMetric.py:6 | Complexity: Beginner | Last updated: 2026-05-18*