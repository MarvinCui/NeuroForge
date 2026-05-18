# How To: Dwiconvert Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIConvert inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(allowLossyConversion=dict(argstr='--allowLossyConversion '), args=dict(argstr='%s'), conversionMode=dict(argstr='--conversionMode %s'), environ=dict(nohash=True, usedefault=True), fMRI=dict(argstr='--fMRI '), fslNIFTIFile=dict(argstr='--fslNIFTIFile %s', extensions=None), gradientVectorFile=dict(argstr='--gradientVectorFile %s', hash_files=False), inputBValues=dict(argstr='--inputBValues %s', extensions=None), inputBVectors=dict(argstr='--inputBVectors %s', extensions=None), inputDicomDirectory=dict(argstr='--inputDicomDirectory %s'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), outputBValues=dict(argstr='--outputBValues %s', hash_files=False), outputBVectors=dict(argstr='--outputBVectors %s', hash_files=False), outputDirectory=dict(argstr='--outputDirectory %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), smallGradientThreshold=dict(argstr='--smallGradientThreshold %f'), transposeInputBVectors=dict(argstr='--transposeInputBVectors '), useBMatrixGradientDirections=dict(argstr='--useBMatrixGradientDirections '), useIdentityMeaseurementFrame=dict(argstr='--useIdentityMeaseurementFrame '), writeProtocolGradientsFile=dict(argstr='--writeProtocolGradientsFile '))
```


## Complete Example

```python
# Workflow
input_map = dict(allowLossyConversion=dict(argstr='--allowLossyConversion '), args=dict(argstr='%s'), conversionMode=dict(argstr='--conversionMode %s'), environ=dict(nohash=True, usedefault=True), fMRI=dict(argstr='--fMRI '), fslNIFTIFile=dict(argstr='--fslNIFTIFile %s', extensions=None), gradientVectorFile=dict(argstr='--gradientVectorFile %s', hash_files=False), inputBValues=dict(argstr='--inputBValues %s', extensions=None), inputBVectors=dict(argstr='--inputBVectors %s', extensions=None), inputDicomDirectory=dict(argstr='--inputDicomDirectory %s'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), outputBValues=dict(argstr='--outputBValues %s', hash_files=False), outputBVectors=dict(argstr='--outputBVectors %s', hash_files=False), outputDirectory=dict(argstr='--outputDirectory %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), smallGradientThreshold=dict(argstr='--smallGradientThreshold %f'), transposeInputBVectors=dict(argstr='--transposeInputBVectors '), useBMatrixGradientDirections=dict(argstr='--useBMatrixGradientDirections '), useIdentityMeaseurementFrame=dict(argstr='--useIdentityMeaseurementFrame '), writeProtocolGradientsFile=dict(argstr='--writeProtocolGradientsFile '))
```

## Next Steps


---

*Source: test_auto_DWIConvert.py:6 | Complexity: Beginner | Last updated: 2026-05-18*