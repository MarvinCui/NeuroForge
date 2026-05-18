# How To: Histogrammatching Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test HistogramMatching inputs

## Prerequisites

**Required Modules:**
- `histogrammatching`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-3), numberOfHistogramLevels=dict(argstr='--numberOfHistogramLevels %d'), numberOfMatchPoints=dict(argstr='--numberOfMatchPoints %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), referenceVolume=dict(argstr='%s', extensions=None, position=-2), threshold=dict(argstr='--threshold '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-3), numberOfHistogramLevels=dict(argstr='--numberOfHistogramLevels %d'), numberOfMatchPoints=dict(argstr='--numberOfMatchPoints %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), referenceVolume=dict(argstr='%s', extensions=None, position=-2), threshold=dict(argstr='--threshold '))
```

## Next Steps


---

*Source: test_auto_HistogramMatching.py:6 | Complexity: Beginner | Last updated: 2026-05-18*