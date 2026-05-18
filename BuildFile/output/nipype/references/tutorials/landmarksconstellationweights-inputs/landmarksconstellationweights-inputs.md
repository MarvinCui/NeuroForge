# How To: Landmarksconstellationweights Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test landmarksConstellationWeights inputs

## Prerequisites

**Required Modules:**
- `brains`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(LLSModel=dict(argstr='--LLSModel %s', extensions=None), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputTemplateModel=dict(argstr='--inputTemplateModel %s', extensions=None), inputTrainingList=dict(argstr='--inputTrainingList %s', extensions=None), outputWeightsList=dict(argstr='--outputWeightsList %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(LLSModel=dict(argstr='--LLSModel %s', extensions=None), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputTemplateModel=dict(argstr='--inputTemplateModel %s', extensions=None), inputTrainingList=dict(argstr='--inputTrainingList %s', extensions=None), outputWeightsList=dict(argstr='--outputWeightsList %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_landmarksConstellationWeights.py:6 | Complexity: Beginner | Last updated: 2026-05-18*