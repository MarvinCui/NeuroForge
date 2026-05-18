# How To: Similarityindex Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SimilarityIndex inputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(ANNContinuousVolume=dict(argstr='--ANNContinuousVolume %s', extensions=None), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputManualVolume=dict(argstr='--inputManualVolume %s', extensions=None), outputCSVFilename=dict(argstr='--outputCSVFilename %s', extensions=None), thresholdInterval=dict(argstr='--thresholdInterval %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(ANNContinuousVolume=dict(argstr='--ANNContinuousVolume %s', extensions=None), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputManualVolume=dict(argstr='--inputManualVolume %s', extensions=None), outputCSVFilename=dict(argstr='--outputCSVFilename %s', extensions=None), thresholdInterval=dict(argstr='--thresholdInterval %f'))
```

## Next Steps


---

*Source: test_auto_SimilarityIndex.py:6 | Complexity: Beginner | Last updated: 2026-05-18*