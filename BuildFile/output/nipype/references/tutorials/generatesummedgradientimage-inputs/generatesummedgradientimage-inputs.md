# How To: Generatesummedgradientimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GenerateSummedGradientImage inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(MaximumGradient=dict(argstr='--MaximumGradient '), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume1=dict(argstr='--inputVolume1 %s', extensions=None), inputVolume2=dict(argstr='--inputVolume2 %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputFileName=dict(argstr='--outputFileName %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(MaximumGradient=dict(argstr='--MaximumGradient '), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume1=dict(argstr='--inputVolume1 %s', extensions=None), inputVolume2=dict(argstr='--inputVolume2 %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputFileName=dict(argstr='--outputFileName %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_GenerateSummedGradientImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*