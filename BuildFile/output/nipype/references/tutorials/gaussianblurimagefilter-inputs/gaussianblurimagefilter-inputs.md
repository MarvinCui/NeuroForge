# How To: Gaussianblurimagefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GaussianBlurImageFilter inputs

## Prerequisites

**Required Modules:**
- `denoising`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), outputVolume=dict(argstr='%s', hash_files=False, position=-1), sigma=dict(argstr='--sigma %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), outputVolume=dict(argstr='%s', hash_files=False, position=-1), sigma=dict(argstr='--sigma %f'))
```

## Next Steps


---

*Source: test_auto_GaussianBlurImageFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*