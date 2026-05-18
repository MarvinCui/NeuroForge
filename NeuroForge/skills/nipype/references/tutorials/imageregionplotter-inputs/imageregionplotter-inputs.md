# How To: Imageregionplotter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ImageRegionPlotter inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputBinaryROIVolume=dict(argstr='--inputBinaryROIVolume %s', extensions=None), inputLabelVolume=dict(argstr='--inputLabelVolume %s', extensions=None), inputVolume1=dict(argstr='--inputVolume1 %s', extensions=None), inputVolume2=dict(argstr='--inputVolume2 %s', extensions=None), numberOfHistogramBins=dict(argstr='--numberOfHistogramBins %d'), outputJointHistogramData=dict(argstr='--outputJointHistogramData %s'), useIntensityForHistogram=dict(argstr='--useIntensityForHistogram '), useROIAUTO=dict(argstr='--useROIAUTO '), verbose=dict(argstr='--verbose '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputBinaryROIVolume=dict(argstr='--inputBinaryROIVolume %s', extensions=None), inputLabelVolume=dict(argstr='--inputLabelVolume %s', extensions=None), inputVolume1=dict(argstr='--inputVolume1 %s', extensions=None), inputVolume2=dict(argstr='--inputVolume2 %s', extensions=None), numberOfHistogramBins=dict(argstr='--numberOfHistogramBins %d'), outputJointHistogramData=dict(argstr='--outputJointHistogramData %s'), useIntensityForHistogram=dict(argstr='--useIntensityForHistogram '), useROIAUTO=dict(argstr='--useROIAUTO '), verbose=dict(argstr='--verbose '))
```

## Next Steps


---

*Source: test_auto_ImageRegionPlotter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*