# How To: Brainsconstellationmodeler Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSConstellationModeler inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(BackgroundFillValue=dict(argstr='--BackgroundFillValue %s'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputTrainingList=dict(argstr='--inputTrainingList %s', extensions=None), mspQualityLevel=dict(argstr='--mspQualityLevel %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), optimizedLandmarksFilenameExtender=dict(argstr='--optimizedLandmarksFilenameExtender %s'), outputModel=dict(argstr='--outputModel %s', hash_files=False), rescaleIntensities=dict(argstr='--rescaleIntensities '), rescaleIntensitiesOutputRange=dict(argstr='--rescaleIntensitiesOutputRange %s', sep=','), resultsDir=dict(argstr='--resultsDir %s', hash_files=False), saveOptimizedLandmarks=dict(argstr='--saveOptimizedLandmarks '), trimRescaledIntensities=dict(argstr='--trimRescaledIntensities %f'), verbose=dict(argstr='--verbose '), writedebuggingImagesLevel=dict(argstr='--writedebuggingImagesLevel %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(BackgroundFillValue=dict(argstr='--BackgroundFillValue %s'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputTrainingList=dict(argstr='--inputTrainingList %s', extensions=None), mspQualityLevel=dict(argstr='--mspQualityLevel %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), optimizedLandmarksFilenameExtender=dict(argstr='--optimizedLandmarksFilenameExtender %s'), outputModel=dict(argstr='--outputModel %s', hash_files=False), rescaleIntensities=dict(argstr='--rescaleIntensities '), rescaleIntensitiesOutputRange=dict(argstr='--rescaleIntensitiesOutputRange %s', sep=','), resultsDir=dict(argstr='--resultsDir %s', hash_files=False), saveOptimizedLandmarks=dict(argstr='--saveOptimizedLandmarks '), trimRescaledIntensities=dict(argstr='--trimRescaledIntensities %f'), verbose=dict(argstr='--verbose '), writedebuggingImagesLevel=dict(argstr='--writedebuggingImagesLevel %d'))
```

## Next Steps


---

*Source: test_auto_BRAINSConstellationModeler.py:6 | Complexity: Beginner | Last updated: 2026-05-18*