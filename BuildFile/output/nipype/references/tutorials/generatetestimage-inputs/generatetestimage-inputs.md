# How To: Generatetestimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GenerateTestImage inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), lowerBoundOfOutputVolume=dict(argstr='--lowerBoundOfOutputVolume %f'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), outputVolumeSize=dict(argstr='--outputVolumeSize %f'), upperBoundOfOutputVolume=dict(argstr='--upperBoundOfOutputVolume %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), lowerBoundOfOutputVolume=dict(argstr='--lowerBoundOfOutputVolume %f'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), outputVolumeSize=dict(argstr='--outputVolumeSize %f'), upperBoundOfOutputVolume=dict(argstr='--upperBoundOfOutputVolume %f'))
```

## Next Steps


---

*Source: test_auto_GenerateTestImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*