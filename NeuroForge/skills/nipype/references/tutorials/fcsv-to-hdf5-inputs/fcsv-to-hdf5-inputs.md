# How To: Fcsv To Hdf5 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test fcsv to hdf5 inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), landmarkGlobPattern=dict(argstr='--landmarkGlobPattern %s'), landmarkTypesList=dict(argstr='--landmarkTypesList %s', extensions=None), landmarksInformationFile=dict(argstr='--landmarksInformationFile %s', hash_files=False), modelFile=dict(argstr='--modelFile %s', hash_files=False), numberOfThreads=dict(argstr='--numberOfThreads %d'), versionID=dict(argstr='--versionID %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), landmarkGlobPattern=dict(argstr='--landmarkGlobPattern %s'), landmarkTypesList=dict(argstr='--landmarkTypesList %s', extensions=None), landmarksInformationFile=dict(argstr='--landmarksInformationFile %s', hash_files=False), modelFile=dict(argstr='--modelFile %s', hash_files=False), numberOfThreads=dict(argstr='--numberOfThreads %d'), versionID=dict(argstr='--versionID %s'))
```

## Next Steps


---

*Source: test_auto_fcsv_to_hdf5.py:6 | Complexity: Beginner | Last updated: 2026-05-18*