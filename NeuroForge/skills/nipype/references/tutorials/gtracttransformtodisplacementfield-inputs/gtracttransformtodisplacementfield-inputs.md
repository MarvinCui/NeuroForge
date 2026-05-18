# How To: Gtracttransformtodisplacementfield Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractTransformToDisplacementField inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), inputTransform=dict(argstr='--inputTransform %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputDeformationFieldVolume=dict(argstr='--outputDeformationFieldVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputReferenceVolume=dict(argstr='--inputReferenceVolume %s', extensions=None), inputTransform=dict(argstr='--inputTransform %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputDeformationFieldVolume=dict(argstr='--outputDeformationFieldVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_gtractTransformToDisplacementField.py:6 | Complexity: Beginner | Last updated: 2026-05-18*