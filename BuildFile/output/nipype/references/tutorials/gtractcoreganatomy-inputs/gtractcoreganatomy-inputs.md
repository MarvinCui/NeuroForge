# How To: Gtractcoreganatomy Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractCoRegAnatomy inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), borderSize=dict(argstr='--borderSize %d'), convergence=dict(argstr='--convergence %f'), environ=dict(nohash=True, usedefault=True), gradientTolerance=dict(argstr='--gradientTolerance %f'), gridSize=dict(argstr='--gridSize %s', sep=','), inputAnatomicalVolume=dict(argstr='--inputAnatomicalVolume %s', extensions=None), inputRigidTransform=dict(argstr='--inputRigidTransform %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maxBSplineDisplacement=dict(argstr='--maxBSplineDisplacement %f'), maximumStepSize=dict(argstr='--maximumStepSize %f'), minimumStepSize=dict(argstr='--minimumStepSize %f'), numberOfHistogramBins=dict(argstr='--numberOfHistogramBins %d'), numberOfIterations=dict(argstr='--numberOfIterations %d'), numberOfSamples=dict(argstr='--numberOfSamples %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTransformName=dict(argstr='--outputTransformName %s', hash_files=False), relaxationFactor=dict(argstr='--relaxationFactor %f'), samplingPercentage=dict(argstr='--samplingPercentage %f'), spatialScale=dict(argstr='--spatialScale %d'), transformType=dict(argstr='--transformType %s'), translationScale=dict(argstr='--translationScale %f'), useCenterOfHeadAlign=dict(argstr='--useCenterOfHeadAlign '), useGeometryAlign=dict(argstr='--useGeometryAlign '), useMomentsAlign=dict(argstr='--useMomentsAlign '), vectorIndex=dict(argstr='--vectorIndex %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), borderSize=dict(argstr='--borderSize %d'), convergence=dict(argstr='--convergence %f'), environ=dict(nohash=True, usedefault=True), gradientTolerance=dict(argstr='--gradientTolerance %f'), gridSize=dict(argstr='--gridSize %s', sep=','), inputAnatomicalVolume=dict(argstr='--inputAnatomicalVolume %s', extensions=None), inputRigidTransform=dict(argstr='--inputRigidTransform %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maxBSplineDisplacement=dict(argstr='--maxBSplineDisplacement %f'), maximumStepSize=dict(argstr='--maximumStepSize %f'), minimumStepSize=dict(argstr='--minimumStepSize %f'), numberOfHistogramBins=dict(argstr='--numberOfHistogramBins %d'), numberOfIterations=dict(argstr='--numberOfIterations %d'), numberOfSamples=dict(argstr='--numberOfSamples %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTransformName=dict(argstr='--outputTransformName %s', hash_files=False), relaxationFactor=dict(argstr='--relaxationFactor %f'), samplingPercentage=dict(argstr='--samplingPercentage %f'), spatialScale=dict(argstr='--spatialScale %d'), transformType=dict(argstr='--transformType %s'), translationScale=dict(argstr='--translationScale %f'), useCenterOfHeadAlign=dict(argstr='--useCenterOfHeadAlign '), useGeometryAlign=dict(argstr='--useGeometryAlign '), useMomentsAlign=dict(argstr='--useMomentsAlign '), vectorIndex=dict(argstr='--vectorIndex %d'))
```

## Next Steps


---

*Source: test_auto_gtractCoRegAnatomy.py:6 | Complexity: Beginner | Last updated: 2026-05-18*