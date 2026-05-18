# How To: Cannyedge Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CannyEdge inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), lowerThreshold=dict(argstr='--lowerThreshold %f'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), upperThreshold=dict(argstr='--upperThreshold %f'), variance=dict(argstr='--variance %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), lowerThreshold=dict(argstr='--lowerThreshold %f'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), upperThreshold=dict(argstr='--upperThreshold %f'), variance=dict(argstr='--variance %f'))
```

## Next Steps


---

*Source: test_auto_CannyEdge.py:6 | Complexity: Beginner | Last updated: 2026-05-18*