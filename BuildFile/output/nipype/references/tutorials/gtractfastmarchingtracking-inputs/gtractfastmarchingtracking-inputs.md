# How To: Gtractfastmarchingtracking Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractFastMarchingTracking inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), costStepSize=dict(argstr='--costStepSize %f'), environ=dict(nohash=True, usedefault=True), inputAnisotropyVolume=dict(argstr='--inputAnisotropyVolume %s', extensions=None), inputCostVolume=dict(argstr='--inputCostVolume %s', extensions=None), inputStartingSeedsLabelMapVolume=dict(argstr='--inputStartingSeedsLabelMapVolume %s', extensions=None), inputTensorVolume=dict(argstr='--inputTensorVolume %s', extensions=None), maximumStepSize=dict(argstr='--maximumStepSize %f'), minimumStepSize=dict(argstr='--minimumStepSize %f'), numberOfIterations=dict(argstr='--numberOfIterations %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTract=dict(argstr='--outputTract %s', hash_files=False), seedThreshold=dict(argstr='--seedThreshold %f'), startingSeedsLabel=dict(argstr='--startingSeedsLabel %d'), trackingThreshold=dict(argstr='--trackingThreshold %f'), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), costStepSize=dict(argstr='--costStepSize %f'), environ=dict(nohash=True, usedefault=True), inputAnisotropyVolume=dict(argstr='--inputAnisotropyVolume %s', extensions=None), inputCostVolume=dict(argstr='--inputCostVolume %s', extensions=None), inputStartingSeedsLabelMapVolume=dict(argstr='--inputStartingSeedsLabelMapVolume %s', extensions=None), inputTensorVolume=dict(argstr='--inputTensorVolume %s', extensions=None), maximumStepSize=dict(argstr='--maximumStepSize %f'), minimumStepSize=dict(argstr='--minimumStepSize %f'), numberOfIterations=dict(argstr='--numberOfIterations %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTract=dict(argstr='--outputTract %s', hash_files=False), seedThreshold=dict(argstr='--seedThreshold %f'), startingSeedsLabel=dict(argstr='--startingSeedsLabel %d'), trackingThreshold=dict(argstr='--trackingThreshold %f'), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```

## Next Steps


---

*Source: test_auto_gtractFastMarchingTracking.py:6 | Complexity: Beginner | Last updated: 2026-05-18*