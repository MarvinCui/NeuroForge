# How To: Gtractfibertracking Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractFiberTracking inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), branchingAngle=dict(argstr='--branchingAngle %f'), branchingThreshold=dict(argstr='--branchingThreshold %f'), curvatureThreshold=dict(argstr='--curvatureThreshold %f'), endingSeedsLabel=dict(argstr='--endingSeedsLabel %d'), environ=dict(nohash=True, usedefault=True), guidedCurvatureThreshold=dict(argstr='--guidedCurvatureThreshold %f'), inputAnisotropyVolume=dict(argstr='--inputAnisotropyVolume %s', extensions=None), inputEndingSeedsLabelMapVolume=dict(argstr='--inputEndingSeedsLabelMapVolume %s', extensions=None), inputStartingSeedsLabelMapVolume=dict(argstr='--inputStartingSeedsLabelMapVolume %s', extensions=None), inputTensorVolume=dict(argstr='--inputTensorVolume %s', extensions=None), inputTract=dict(argstr='--inputTract %s', extensions=None), maximumBranchPoints=dict(argstr='--maximumBranchPoints %d'), maximumGuideDistance=dict(argstr='--maximumGuideDistance %f'), maximumLength=dict(argstr='--maximumLength %f'), minimumLength=dict(argstr='--minimumLength %f'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTract=dict(argstr='--outputTract %s', hash_files=False), randomSeed=dict(argstr='--randomSeed %d'), seedThreshold=dict(argstr='--seedThreshold %f'), startingSeedsLabel=dict(argstr='--startingSeedsLabel %d'), stepSize=dict(argstr='--stepSize %f'), tendF=dict(argstr='--tendF %f'), tendG=dict(argstr='--tendG %f'), trackingMethod=dict(argstr='--trackingMethod %s'), trackingThreshold=dict(argstr='--trackingThreshold %f'), useLoopDetection=dict(argstr='--useLoopDetection '), useRandomWalk=dict(argstr='--useRandomWalk '), useTend=dict(argstr='--useTend '), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), branchingAngle=dict(argstr='--branchingAngle %f'), branchingThreshold=dict(argstr='--branchingThreshold %f'), curvatureThreshold=dict(argstr='--curvatureThreshold %f'), endingSeedsLabel=dict(argstr='--endingSeedsLabel %d'), environ=dict(nohash=True, usedefault=True), guidedCurvatureThreshold=dict(argstr='--guidedCurvatureThreshold %f'), inputAnisotropyVolume=dict(argstr='--inputAnisotropyVolume %s', extensions=None), inputEndingSeedsLabelMapVolume=dict(argstr='--inputEndingSeedsLabelMapVolume %s', extensions=None), inputStartingSeedsLabelMapVolume=dict(argstr='--inputStartingSeedsLabelMapVolume %s', extensions=None), inputTensorVolume=dict(argstr='--inputTensorVolume %s', extensions=None), inputTract=dict(argstr='--inputTract %s', extensions=None), maximumBranchPoints=dict(argstr='--maximumBranchPoints %d'), maximumGuideDistance=dict(argstr='--maximumGuideDistance %f'), maximumLength=dict(argstr='--maximumLength %f'), minimumLength=dict(argstr='--minimumLength %f'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTract=dict(argstr='--outputTract %s', hash_files=False), randomSeed=dict(argstr='--randomSeed %d'), seedThreshold=dict(argstr='--seedThreshold %f'), startingSeedsLabel=dict(argstr='--startingSeedsLabel %d'), stepSize=dict(argstr='--stepSize %f'), tendF=dict(argstr='--tendF %f'), tendG=dict(argstr='--tendG %f'), trackingMethod=dict(argstr='--trackingMethod %s'), trackingThreshold=dict(argstr='--trackingThreshold %f'), useLoopDetection=dict(argstr='--useLoopDetection '), useRandomWalk=dict(argstr='--useRandomWalk '), useTend=dict(argstr='--useTend '), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```

## Next Steps


---

*Source: test_auto_gtractFiberTracking.py:6 | Complexity: Beginner | Last updated: 2026-05-18*