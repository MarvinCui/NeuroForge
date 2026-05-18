# How To: Extractskeleton Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ExtractSkeleton inputs

## Prerequisites

**Required Modules:**
- `extractskeleton`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputImageFileName=dict(argstr='%s', extensions=None, position=-2), OutputImageFileName=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), dontPrune=dict(argstr='--dontPrune '), environ=dict(nohash=True, usedefault=True), numPoints=dict(argstr='--numPoints %d'), pointsFile=dict(argstr='--pointsFile %s'), type=dict(argstr='--type %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(InputImageFileName=dict(argstr='%s', extensions=None, position=-2), OutputImageFileName=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), dontPrune=dict(argstr='--dontPrune '), environ=dict(nohash=True, usedefault=True), numPoints=dict(argstr='--numPoints %d'), pointsFile=dict(argstr='--pointsFile %s'), type=dict(argstr='--type %s'))
```

## Next Steps


---

*Source: test_auto_ExtractSkeleton.py:6 | Complexity: Beginner | Last updated: 2026-05-18*