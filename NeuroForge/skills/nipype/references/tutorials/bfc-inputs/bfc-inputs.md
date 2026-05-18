# How To: Bfc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Bfc inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), biasEstimateConvergenceThreshold=dict(argstr='--beps %f'), biasEstimateSpacing=dict(argstr='-s %d'), biasFieldEstimatesOutputPrefix=dict(argstr='--biasprefix %s'), biasRange=dict(argstr='%s'), controlPointSpacing=dict(argstr='-c %d'), convergenceThreshold=dict(argstr='--eps %f'), correctWholeVolume=dict(argstr='--extrapolate'), correctedImagesOutputPrefix=dict(argstr='--prefix %s'), correctionScheduleFile=dict(argstr='--schedule %s', extensions=None), environ=dict(nohash=True, usedefault=True), histogramRadius=dict(argstr='-r %d'), histogramType=dict(argstr='%s'), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), inputMaskFile=dict(argstr='-m %s', extensions=None, hash_files=False), intermediate_file_type=dict(argstr='%s'), iterativeMode=dict(argstr='--iterate'), maxBias=dict(argstr='-U %f', usedefault=True), minBias=dict(argstr='-L %f', usedefault=True), outputBiasField=dict(argstr='--bias %s', extensions=None, hash_files=False), outputMRIVolume=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), outputMaskedBiasField=dict(argstr='--maskedbias %s', extensions=None, hash_files=False), splineLambda=dict(argstr='-w %f'), timer=dict(argstr='--timer'), verbosityLevel=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), biasEstimateConvergenceThreshold=dict(argstr='--beps %f'), biasEstimateSpacing=dict(argstr='-s %d'), biasFieldEstimatesOutputPrefix=dict(argstr='--biasprefix %s'), biasRange=dict(argstr='%s'), controlPointSpacing=dict(argstr='-c %d'), convergenceThreshold=dict(argstr='--eps %f'), correctWholeVolume=dict(argstr='--extrapolate'), correctedImagesOutputPrefix=dict(argstr='--prefix %s'), correctionScheduleFile=dict(argstr='--schedule %s', extensions=None), environ=dict(nohash=True, usedefault=True), histogramRadius=dict(argstr='-r %d'), histogramType=dict(argstr='%s'), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), inputMaskFile=dict(argstr='-m %s', extensions=None, hash_files=False), intermediate_file_type=dict(argstr='%s'), iterativeMode=dict(argstr='--iterate'), maxBias=dict(argstr='-U %f', usedefault=True), minBias=dict(argstr='-L %f', usedefault=True), outputBiasField=dict(argstr='--bias %s', extensions=None, hash_files=False), outputMRIVolume=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), outputMaskedBiasField=dict(argstr='--maskedbias %s', extensions=None, hash_files=False), splineLambda=dict(argstr='-w %f'), timer=dict(argstr='--timer'), verbosityLevel=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Bfc.py:6 | Complexity: Beginner | Last updated: 2026-05-18*