# How To: Brainstransformconvert Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSTransformConvert inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), displacementVolume=dict(argstr='--displacementVolume %s', hash_files=False), environ=dict(nohash=True, usedefault=True), inputTransform=dict(argstr='--inputTransform %s', extensions=None), outputPrecisionType=dict(argstr='--outputPrecisionType %s'), outputTransform=dict(argstr='--outputTransform %s', hash_files=False), outputTransformType=dict(argstr='--outputTransformType %s'), referenceVolume=dict(argstr='--referenceVolume %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), displacementVolume=dict(argstr='--displacementVolume %s', hash_files=False), environ=dict(nohash=True, usedefault=True), inputTransform=dict(argstr='--inputTransform %s', extensions=None), outputPrecisionType=dict(argstr='--outputPrecisionType %s'), outputTransform=dict(argstr='--outputTransform %s', hash_files=False), outputTransformType=dict(argstr='--outputTransformType %s'), referenceVolume=dict(argstr='--referenceVolume %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_BRAINSTransformConvert.py:6 | Complexity: Beginner | Last updated: 2026-05-18*