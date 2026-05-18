# How To: Brainsmush Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSMush inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), boundingBoxSize=dict(argstr='--boundingBoxSize %s', sep=','), boundingBoxStart=dict(argstr='--boundingBoxStart %s', sep=','), desiredMean=dict(argstr='--desiredMean %f'), desiredVariance=dict(argstr='--desiredVariance %f'), environ=dict(nohash=True, usedefault=True), inputFirstVolume=dict(argstr='--inputFirstVolume %s', extensions=None), inputMaskVolume=dict(argstr='--inputMaskVolume %s', extensions=None), inputSecondVolume=dict(argstr='--inputSecondVolume %s', extensions=None), lowerThresholdFactor=dict(argstr='--lowerThresholdFactor %f'), lowerThresholdFactorPre=dict(argstr='--lowerThresholdFactorPre %f'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputMask=dict(argstr='--outputMask %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), outputWeightsFile=dict(argstr='--outputWeightsFile %s', hash_files=False), seed=dict(argstr='--seed %s', sep=','), upperThresholdFactor=dict(argstr='--upperThresholdFactor %f'), upperThresholdFactorPre=dict(argstr='--upperThresholdFactorPre %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), boundingBoxSize=dict(argstr='--boundingBoxSize %s', sep=','), boundingBoxStart=dict(argstr='--boundingBoxStart %s', sep=','), desiredMean=dict(argstr='--desiredMean %f'), desiredVariance=dict(argstr='--desiredVariance %f'), environ=dict(nohash=True, usedefault=True), inputFirstVolume=dict(argstr='--inputFirstVolume %s', extensions=None), inputMaskVolume=dict(argstr='--inputMaskVolume %s', extensions=None), inputSecondVolume=dict(argstr='--inputSecondVolume %s', extensions=None), lowerThresholdFactor=dict(argstr='--lowerThresholdFactor %f'), lowerThresholdFactorPre=dict(argstr='--lowerThresholdFactorPre %f'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputMask=dict(argstr='--outputMask %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), outputWeightsFile=dict(argstr='--outputWeightsFile %s', hash_files=False), seed=dict(argstr='--seed %s', sep=','), upperThresholdFactor=dict(argstr='--upperThresholdFactor %f'), upperThresholdFactorPre=dict(argstr='--upperThresholdFactorPre %f'))
```

## Next Steps


---

*Source: test_auto_BRAINSMush.py:6 | Complexity: Beginner | Last updated: 2026-05-18*