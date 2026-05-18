# How To: Generatebrainclippedimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GenerateBrainClippedImage inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputImg=dict(argstr='--inputImg %s', extensions=None), inputMsk=dict(argstr='--inputMsk %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputFileName=dict(argstr='--outputFileName %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputImg=dict(argstr='--inputImg %s', extensions=None), inputMsk=dict(argstr='--inputMsk %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputFileName=dict(argstr='--outputFileName %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_GenerateBrainClippedImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*