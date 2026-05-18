# How To: Gtractimageconformity Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractImageConformity inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_gtractImageConformity.py:6 | Complexity: Beginner | Last updated: 2026-05-18*