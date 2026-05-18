# How To: Otsuthresholdimagefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test OtsuThresholdImageFilter inputs

## Prerequisites

**Required Modules:**
- `filtering`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), insideValue=dict(argstr='--insideValue %d'), numberOfBins=dict(argstr='--numberOfBins %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), outsideValue=dict(argstr='--outsideValue %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), insideValue=dict(argstr='--insideValue %d'), numberOfBins=dict(argstr='--numberOfBins %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), outsideValue=dict(argstr='--outsideValue %d'))
```

## Next Steps


---

*Source: test_auto_OtsuThresholdImageFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*