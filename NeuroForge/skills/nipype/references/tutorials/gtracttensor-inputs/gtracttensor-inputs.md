# How To: Gtracttensor Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractTensor inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(applyMeasurementFrame=dict(argstr='--applyMeasurementFrame '), args=dict(argstr='%s'), b0Index=dict(argstr='--b0Index %d'), backgroundSuppressingThreshold=dict(argstr='--backgroundSuppressingThreshold %d'), environ=dict(nohash=True, usedefault=True), ignoreIndex=dict(argstr='--ignoreIndex %s', sep=','), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maskProcessingMode=dict(argstr='--maskProcessingMode %s'), maskVolume=dict(argstr='--maskVolume %s', extensions=None), medianFilterSize=dict(argstr='--medianFilterSize %s', sep=','), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), resampleIsotropic=dict(argstr='--resampleIsotropic '), size=dict(argstr='--size %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(applyMeasurementFrame=dict(argstr='--applyMeasurementFrame '), args=dict(argstr='%s'), b0Index=dict(argstr='--b0Index %d'), backgroundSuppressingThreshold=dict(argstr='--backgroundSuppressingThreshold %d'), environ=dict(nohash=True, usedefault=True), ignoreIndex=dict(argstr='--ignoreIndex %s', sep=','), inputVolume=dict(argstr='--inputVolume %s', extensions=None), maskProcessingMode=dict(argstr='--maskProcessingMode %s'), maskVolume=dict(argstr='--maskVolume %s', extensions=None), medianFilterSize=dict(argstr='--medianFilterSize %s', sep=','), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), resampleIsotropic=dict(argstr='--resampleIsotropic '), size=dict(argstr='--size %f'))
```

## Next Steps


---

*Source: test_auto_gtractTensor.py:6 | Complexity: Beginner | Last updated: 2026-05-18*