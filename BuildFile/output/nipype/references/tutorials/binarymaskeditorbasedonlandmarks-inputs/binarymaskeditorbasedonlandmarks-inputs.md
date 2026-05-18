# How To: Binarymaskeditorbasedonlandmarks Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BinaryMaskEditorBasedOnLandmarks inputs

## Prerequisites

**Required Modules:**
- `specialized`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputBinaryVolume=dict(argstr='--inputBinaryVolume %s', extensions=None), inputLandmarkNames=dict(argstr='--inputLandmarkNames %s', sep=','), inputLandmarkNamesForObliquePlane=dict(argstr='--inputLandmarkNamesForObliquePlane %s', sep=','), inputLandmarksFilename=dict(argstr='--inputLandmarksFilename %s', extensions=None), outputBinaryVolume=dict(argstr='--outputBinaryVolume %s', hash_files=False), setCutDirectionForLandmark=dict(argstr='--setCutDirectionForLandmark %s', sep=','), setCutDirectionForObliquePlane=dict(argstr='--setCutDirectionForObliquePlane %s', sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputBinaryVolume=dict(argstr='--inputBinaryVolume %s', extensions=None), inputLandmarkNames=dict(argstr='--inputLandmarkNames %s', sep=','), inputLandmarkNamesForObliquePlane=dict(argstr='--inputLandmarkNamesForObliquePlane %s', sep=','), inputLandmarksFilename=dict(argstr='--inputLandmarksFilename %s', extensions=None), outputBinaryVolume=dict(argstr='--outputBinaryVolume %s', hash_files=False), setCutDirectionForLandmark=dict(argstr='--setCutDirectionForLandmark %s', sep=','), setCutDirectionForObliquePlane=dict(argstr='--setCutDirectionForObliquePlane %s', sep=','))
```

## Next Steps


---

*Source: test_auto_BinaryMaskEditorBasedOnLandmarks.py:6 | Complexity: Beginner | Last updated: 2026-05-18*