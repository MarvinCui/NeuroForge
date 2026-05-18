# How To: Texturemeasurefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TextureMeasureFilter inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), distance=dict(argstr='--distance %d'), environ=dict(nohash=True, usedefault=True), inputMaskVolume=dict(argstr='--inputMaskVolume %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), insideROIValue=dict(argstr='--insideROIValue %f'), outputFilename=dict(argstr='--outputFilename %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), distance=dict(argstr='--distance %d'), environ=dict(nohash=True, usedefault=True), inputMaskVolume=dict(argstr='--inputMaskVolume %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), insideROIValue=dict(argstr='--insideROIValue %f'), outputFilename=dict(argstr='--outputFilename %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_TextureMeasureFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*