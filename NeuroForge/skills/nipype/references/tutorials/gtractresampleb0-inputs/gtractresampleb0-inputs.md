# How To: Gtractresampleb0 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractResampleB0 inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputAnatomicalVolume=dict(argstr='--inputAnatomicalVolume %s', extensions=None), inputTransform=dict(argstr='--inputTransform %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), transformType=dict(argstr='--transformType %s'), vectorIndex=dict(argstr='--vectorIndex %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputAnatomicalVolume=dict(argstr='--inputAnatomicalVolume %s', extensions=None), inputTransform=dict(argstr='--inputTransform %s', extensions=None), inputVolume=dict(argstr='--inputVolume %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), transformType=dict(argstr='--transformType %s'), vectorIndex=dict(argstr='--vectorIndex %d'))
```

## Next Steps


---

*Source: test_auto_gtractResampleB0.py:6 | Complexity: Beginner | Last updated: 2026-05-18*