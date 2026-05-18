# How To: Gtractresamplecodeimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractResampleCodeImage inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputCodeVolume=dict(argstr='--inputCodeVolume %s', extensions=None), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), inputTransform=dict(argstr='--inputTransform %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), transformType=dict(argstr='--transformType %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputCodeVolume=dict(argstr='--inputCodeVolume %s', extensions=None), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), inputTransform=dict(argstr='--inputTransform %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), transformType=dict(argstr='--transformType %s'))
```

## Next Steps


---

*Source: test_auto_gtractResampleCodeImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*