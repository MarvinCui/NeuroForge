# How To: Robuststatisticssegmenter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RobustStatisticsSegmenter inputs

## Prerequisites

**Required Modules:**
- `specialized`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), curvatureWeight=dict(argstr='--curvatureWeight %f'), environ=dict(nohash=True, usedefault=True), expectedVolume=dict(argstr='--expectedVolume %f'), intensityHomogeneity=dict(argstr='--intensityHomogeneity %f'), labelImageFileName=dict(argstr='%s', extensions=None, position=-2), labelValue=dict(argstr='--labelValue %d'), maxRunningTime=dict(argstr='--maxRunningTime %f'), originalImageFileName=dict(argstr='%s', extensions=None, position=-3), segmentedImageFileName=dict(argstr='%s', hash_files=False, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), curvatureWeight=dict(argstr='--curvatureWeight %f'), environ=dict(nohash=True, usedefault=True), expectedVolume=dict(argstr='--expectedVolume %f'), intensityHomogeneity=dict(argstr='--intensityHomogeneity %f'), labelImageFileName=dict(argstr='%s', extensions=None, position=-2), labelValue=dict(argstr='--labelValue %d'), maxRunningTime=dict(argstr='--maxRunningTime %f'), originalImageFileName=dict(argstr='%s', extensions=None, position=-3), segmentedImageFileName=dict(argstr='%s', hash_files=False, position=-1))
```

## Next Steps


---

*Source: test_auto_RobustStatisticsSegmenter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*