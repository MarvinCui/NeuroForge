# How To: Brainsdemonwarp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSDemonWarp inputs

## Prerequisites

**Required Modules:**
- `specialized`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), arrayOfPyramidLevelIterations=dict(argstr='--arrayOfPyramidLevelIterations %s', sep=','), backgroundFillValue=dict(argstr='--backgroundFillValue %d'), checkerboardPatternSubdivisions=dict(argstr='--checkerboardPatternSubdivisions %s', sep=','), environ=dict(nohash=True, usedefault=True), fixedBinaryVolume=dict(argstr='--fixedBinaryVolume %s', extensions=None), fixedVolume=dict(argstr='--fixedVolume %s', extensions=None), gradient_type=dict(argstr='--gradient_type %s'), gui=dict(argstr='--gui '), histogramMatch=dict(argstr='--histogramMatch '), initializeWithDisplacementField=dict(argstr='--initializeWithDisplacementField %s', extensions=None), initializeWithTransform=dict(argstr='--initializeWithTransform %s', extensions=None), inputPixelType=dict(argstr='--inputPixelType %s'), interpolationMode=dict(argstr='--interpolationMode %s'), lowerThresholdForBOBF=dict(argstr='--lowerThresholdForBOBF %d'), maskProcessingMode=dict(argstr='--maskProcessingMode %s'), max_step_length=dict(argstr='--max_step_length %f'), medianFilterSize=dict(argstr='--medianFilterSize %s', sep=','), minimumFixedPyramid=dict(argstr='--minimumFixedPyramid %s', sep=','), minimumMovingPyramid=dict(argstr='--minimumMovingPyramid %s', sep=','), movingBinaryVolume=dict(argstr='--movingBinaryVolume %s', extensions=None), movingVolume=dict(argstr='--movingVolume %s', extensions=None), neighborhoodForBOBF=dict(argstr='--neighborhoodForBOBF %s', sep=','), numberOfBCHApproximationTerms=dict(argstr='--numberOfBCHApproximationTerms %d'), numberOfHistogramBins=dict(argstr='--numberOfHistogramBins %d'), numberOfMatchPoints=dict(argstr='--numberOfMatchPoints %d'), numberOfPyramidLevels=dict(argstr='--numberOfPyramidLevels %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputCheckerboardVolume=dict(argstr='--outputCheckerboardVolume %s', hash_files=False), outputDebug=dict(argstr='--outputDebug '), outputDisplacementFieldPrefix=dict(argstr='--outputDisplacementFieldPrefix %s'), outputDisplacementFieldVolume=dict(argstr='--outputDisplacementFieldVolume %s', hash_files=False), outputNormalized=dict(argstr='--outputNormalized '), outputPixelType=dict(argstr='--outputPixelType %s'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), promptUser=dict(argstr='--promptUser '), registrationFilterType=dict(argstr='--registrationFilterType %s'), seedForBOBF=dict(argstr='--seedForBOBF %s', sep=','), smoothDisplacementFieldSigma=dict(argstr='--smoothDisplacementFieldSigma %f'), upFieldSmoothing=dict(argstr='--upFieldSmoothing %f'), upperThresholdForBOBF=dict(argstr='--upperThresholdForBOBF %d'), use_vanilla_dem=dict(argstr='--use_vanilla_dem '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), arrayOfPyramidLevelIterations=dict(argstr='--arrayOfPyramidLevelIterations %s', sep=','), backgroundFillValue=dict(argstr='--backgroundFillValue %d'), checkerboardPatternSubdivisions=dict(argstr='--checkerboardPatternSubdivisions %s', sep=','), environ=dict(nohash=True, usedefault=True), fixedBinaryVolume=dict(argstr='--fixedBinaryVolume %s', extensions=None), fixedVolume=dict(argstr='--fixedVolume %s', extensions=None), gradient_type=dict(argstr='--gradient_type %s'), gui=dict(argstr='--gui '), histogramMatch=dict(argstr='--histogramMatch '), initializeWithDisplacementField=dict(argstr='--initializeWithDisplacementField %s', extensions=None), initializeWithTransform=dict(argstr='--initializeWithTransform %s', extensions=None), inputPixelType=dict(argstr='--inputPixelType %s'), interpolationMode=dict(argstr='--interpolationMode %s'), lowerThresholdForBOBF=dict(argstr='--lowerThresholdForBOBF %d'), maskProcessingMode=dict(argstr='--maskProcessingMode %s'), max_step_length=dict(argstr='--max_step_length %f'), medianFilterSize=dict(argstr='--medianFilterSize %s', sep=','), minimumFixedPyramid=dict(argstr='--minimumFixedPyramid %s', sep=','), minimumMovingPyramid=dict(argstr='--minimumMovingPyramid %s', sep=','), movingBinaryVolume=dict(argstr='--movingBinaryVolume %s', extensions=None), movingVolume=dict(argstr='--movingVolume %s', extensions=None), neighborhoodForBOBF=dict(argstr='--neighborhoodForBOBF %s', sep=','), numberOfBCHApproximationTerms=dict(argstr='--numberOfBCHApproximationTerms %d'), numberOfHistogramBins=dict(argstr='--numberOfHistogramBins %d'), numberOfMatchPoints=dict(argstr='--numberOfMatchPoints %d'), numberOfPyramidLevels=dict(argstr='--numberOfPyramidLevels %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputCheckerboardVolume=dict(argstr='--outputCheckerboardVolume %s', hash_files=False), outputDebug=dict(argstr='--outputDebug '), outputDisplacementFieldPrefix=dict(argstr='--outputDisplacementFieldPrefix %s'), outputDisplacementFieldVolume=dict(argstr='--outputDisplacementFieldVolume %s', hash_files=False), outputNormalized=dict(argstr='--outputNormalized '), outputPixelType=dict(argstr='--outputPixelType %s'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), promptUser=dict(argstr='--promptUser '), registrationFilterType=dict(argstr='--registrationFilterType %s'), seedForBOBF=dict(argstr='--seedForBOBF %s', sep=','), smoothDisplacementFieldSigma=dict(argstr='--smoothDisplacementFieldSigma %f'), upFieldSmoothing=dict(argstr='--upFieldSmoothing %f'), upperThresholdForBOBF=dict(argstr='--upperThresholdForBOBF %d'), use_vanilla_dem=dict(argstr='--use_vanilla_dem '))
```

## Next Steps


---

*Source: test_auto_BRAINSDemonWarp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*