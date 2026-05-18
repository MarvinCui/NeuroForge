# How To: Medianimagefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MedianImageFilter inputs

## Prerequisites

**Required Modules:**
- `denoising`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), neighborhood=dict(argstr='--neighborhood %s', sep=','), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), neighborhood=dict(argstr='--neighborhood %s', sep=','), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```

## Next Steps


---

*Source: test_auto_MedianImageFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*