# How To: Brainsroiauto Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSROIAuto inputs

## Prerequisites

**Required Modules:**
- `specialized`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(ROIAutoDilateSize=dict(argstr='--ROIAutoDilateSize %f'), args=dict(argstr='%s'), closingSize=dict(argstr='--closingSize %f'), cropOutput=dict(argstr='--cropOutput '), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maskOutput=dict(argstr='--maskOutput '), numberOfThreads=dict(argstr='--numberOfThreads %d'), otsuPercentileThreshold=dict(argstr='--otsuPercentileThreshold %f'), outputROIMaskVolume=dict(argstr='--outputROIMaskVolume %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), outputVolumePixelType=dict(argstr='--outputVolumePixelType %s'), thresholdCorrectionFactor=dict(argstr='--thresholdCorrectionFactor %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(ROIAutoDilateSize=dict(argstr='--ROIAutoDilateSize %f'), args=dict(argstr='%s'), closingSize=dict(argstr='--closingSize %f'), cropOutput=dict(argstr='--cropOutput '), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maskOutput=dict(argstr='--maskOutput '), numberOfThreads=dict(argstr='--numberOfThreads %d'), otsuPercentileThreshold=dict(argstr='--otsuPercentileThreshold %f'), outputROIMaskVolume=dict(argstr='--outputROIMaskVolume %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), outputVolumePixelType=dict(argstr='--outputVolumePixelType %s'), thresholdCorrectionFactor=dict(argstr='--thresholdCorrectionFactor %f'))
```

## Next Steps


---

*Source: test_auto_BRAINSROIAuto.py:6 | Complexity: Beginner | Last updated: 2026-05-18*