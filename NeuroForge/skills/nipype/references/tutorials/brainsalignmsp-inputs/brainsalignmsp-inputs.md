# How To: Brainsalignmsp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSAlignMSP inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(BackgroundFillValue=dict(argstr='--BackgroundFillValue %s'), OutputresampleMSP=dict(argstr='--OutputresampleMSP %s', hash_files=False), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), interpolationMode=dict(argstr='--interpolationMode %s'), mspQualityLevel=dict(argstr='--mspQualityLevel %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), rescaleIntensities=dict(argstr='--rescaleIntensities '), rescaleIntensitiesOutputRange=dict(argstr='--rescaleIntensitiesOutputRange %s', sep=','), resultsDir=dict(argstr='--resultsDir %s', hash_files=False), trimRescaledIntensities=dict(argstr='--trimRescaledIntensities %f'), verbose=dict(argstr='--verbose '), writedebuggingImagesLevel=dict(argstr='--writedebuggingImagesLevel %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(BackgroundFillValue=dict(argstr='--BackgroundFillValue %s'), OutputresampleMSP=dict(argstr='--OutputresampleMSP %s', hash_files=False), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), interpolationMode=dict(argstr='--interpolationMode %s'), mspQualityLevel=dict(argstr='--mspQualityLevel %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), rescaleIntensities=dict(argstr='--rescaleIntensities '), rescaleIntensitiesOutputRange=dict(argstr='--rescaleIntensitiesOutputRange %s', sep=','), resultsDir=dict(argstr='--resultsDir %s', hash_files=False), trimRescaledIntensities=dict(argstr='--trimRescaledIntensities %f'), verbose=dict(argstr='--verbose '), writedebuggingImagesLevel=dict(argstr='--writedebuggingImagesLevel %d'))
```

## Next Steps


---

*Source: test_auto_BRAINSAlignMSP.py:6 | Complexity: Beginner | Last updated: 2026-05-18*