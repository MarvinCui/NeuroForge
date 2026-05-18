# How To: Otsuthresholdsegmentation Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test OtsuThresholdSegmentation inputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), brightObjects=dict(argstr='--brightObjects '), environ=dict(nohash=True, usedefault=True), faceConnected=dict(argstr='--faceConnected '), inputVolume=dict(argstr='%s', extensions=None, position=-2), minimumObjectSize=dict(argstr='--minimumObjectSize %d'), numberOfBins=dict(argstr='--numberOfBins %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), brightObjects=dict(argstr='--brightObjects '), environ=dict(nohash=True, usedefault=True), faceConnected=dict(argstr='--faceConnected '), inputVolume=dict(argstr='%s', extensions=None, position=-2), minimumObjectSize=dict(argstr='--minimumObjectSize %d'), numberOfBins=dict(argstr='--numberOfBins %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```

## Next Steps


---

*Source: test_auto_OtsuThresholdSegmentation.py:6 | Complexity: Beginner | Last updated: 2026-05-18*