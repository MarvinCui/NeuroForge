# How To: Gtractcoregbvalues Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractCoregBvalues inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), debugLevel=dict(argstr='--debugLevel %d'), eddyCurrentCorrection=dict(argstr='--eddyCurrentCorrection '), environ=dict(nohash=True, usedefault=True), fixedVolume=dict(argstr='--fixedVolume %s', extensions=None), fixedVolumeIndex=dict(argstr='--fixedVolumeIndex %d'), maximumStepSize=dict(argstr='--maximumStepSize %f'), minimumStepSize=dict(argstr='--minimumStepSize %f'), movingVolume=dict(argstr='--movingVolume %s', extensions=None), numberOfIterations=dict(argstr='--numberOfIterations %d'), numberOfSpatialSamples=dict(argstr='--numberOfSpatialSamples %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTransform=dict(argstr='--outputTransform %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), registerB0Only=dict(argstr='--registerB0Only '), relaxationFactor=dict(argstr='--relaxationFactor %f'), samplingPercentage=dict(argstr='--samplingPercentage %f'), spatialScale=dict(argstr='--spatialScale %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), debugLevel=dict(argstr='--debugLevel %d'), eddyCurrentCorrection=dict(argstr='--eddyCurrentCorrection '), environ=dict(nohash=True, usedefault=True), fixedVolume=dict(argstr='--fixedVolume %s', extensions=None), fixedVolumeIndex=dict(argstr='--fixedVolumeIndex %d'), maximumStepSize=dict(argstr='--maximumStepSize %f'), minimumStepSize=dict(argstr='--minimumStepSize %f'), movingVolume=dict(argstr='--movingVolume %s', extensions=None), numberOfIterations=dict(argstr='--numberOfIterations %d'), numberOfSpatialSamples=dict(argstr='--numberOfSpatialSamples %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTransform=dict(argstr='--outputTransform %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), registerB0Only=dict(argstr='--registerB0Only '), relaxationFactor=dict(argstr='--relaxationFactor %f'), samplingPercentage=dict(argstr='--samplingPercentage %f'), spatialScale=dict(argstr='--spatialScale %f'))
```

## Next Steps


---

*Source: test_auto_gtractCoregBvalues.py:6 | Complexity: Beginner | Last updated: 2026-05-18*