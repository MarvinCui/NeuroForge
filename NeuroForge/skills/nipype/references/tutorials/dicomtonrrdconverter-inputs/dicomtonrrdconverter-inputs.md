# How To: Dicomtonrrdconverter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DicomToNrrdConverter inputs

## Prerequisites

**Required Modules:**
- `converters`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputDicomDirectory=dict(argstr='--inputDicomDirectory %s'), outputDirectory=dict(argstr='--outputDirectory %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s'), smallGradientThreshold=dict(argstr='--smallGradientThreshold %f'), useBMatrixGradientDirections=dict(argstr='--useBMatrixGradientDirections '), useIdentityMeaseurementFrame=dict(argstr='--useIdentityMeaseurementFrame '), writeProtocolGradientsFile=dict(argstr='--writeProtocolGradientsFile '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputDicomDirectory=dict(argstr='--inputDicomDirectory %s'), outputDirectory=dict(argstr='--outputDirectory %s', hash_files=False), outputVolume=dict(argstr='--outputVolume %s'), smallGradientThreshold=dict(argstr='--smallGradientThreshold %f'), useBMatrixGradientDirections=dict(argstr='--useBMatrixGradientDirections '), useIdentityMeaseurementFrame=dict(argstr='--useIdentityMeaseurementFrame '), writeProtocolGradientsFile=dict(argstr='--writeProtocolGradientsFile '))
```

## Next Steps


---

*Source: test_auto_DicomToNrrdConverter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*