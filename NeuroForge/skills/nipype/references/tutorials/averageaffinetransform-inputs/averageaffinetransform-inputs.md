# How To: Averageaffinetransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AverageAffineTransform inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', mandatory=True, position=0), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), output_affine_transform=dict(argstr='%s', extensions=None, mandatory=True, position=1), transforms=dict(argstr='%s', mandatory=True, position=3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%d', mandatory=True, position=0), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), output_affine_transform=dict(argstr='%s', extensions=None, mandatory=True, position=1), transforms=dict(argstr='%s', mandatory=True, position=3))
```

## Next Steps


---

*Source: test_auto_AverageAffineTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*