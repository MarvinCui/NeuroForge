# How To: Gtractcostfastmarching Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractCostFastMarching inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(anisotropyWeight=dict(argstr='--anisotropyWeight %f'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputAnisotropyVolume=dict(argstr='--inputAnisotropyVolume %s', extensions=None), inputStartingSeedsLabelMapVolume=dict(argstr='--inputStartingSeedsLabelMapVolume %s', extensions=None), inputTensorVolume=dict(argstr='--inputTensorVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputCostVolume=dict(argstr='--outputCostVolume %s', hash_files=False), outputSpeedVolume=dict(argstr='--outputSpeedVolume %s', hash_files=False), seedThreshold=dict(argstr='--seedThreshold %f'), startingSeedsLabel=dict(argstr='--startingSeedsLabel %d'), stoppingValue=dict(argstr='--stoppingValue %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(anisotropyWeight=dict(argstr='--anisotropyWeight %f'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputAnisotropyVolume=dict(argstr='--inputAnisotropyVolume %s', extensions=None), inputStartingSeedsLabelMapVolume=dict(argstr='--inputStartingSeedsLabelMapVolume %s', extensions=None), inputTensorVolume=dict(argstr='--inputTensorVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputCostVolume=dict(argstr='--outputCostVolume %s', hash_files=False), outputSpeedVolume=dict(argstr='--outputSpeedVolume %s', hash_files=False), seedThreshold=dict(argstr='--seedThreshold %f'), startingSeedsLabel=dict(argstr='--startingSeedsLabel %d'), stoppingValue=dict(argstr='--stoppingValue %f'))
```

## Next Steps


---

*Source: test_auto_gtractCostFastMarching.py:6 | Complexity: Beginner | Last updated: 2026-05-18*