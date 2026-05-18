# How To: Applytransformstopoints Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ApplyTransformsToPoints inputs

## Prerequisites

**Required Modules:**
- `resampling`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='--dimensionality %d'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='--input %s', extensions=None, mandatory=True), invert_transform_flags=dict(), num_threads=dict(nohash=True, usedefault=True), output_file=dict(argstr='--output %s', hash_files=False, name_source=['input_file'], name_template='%s_transformed.csv'), transforms=dict(argstr='%s', mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='--dimensionality %d'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='--input %s', extensions=None, mandatory=True), invert_transform_flags=dict(), num_threads=dict(nohash=True, usedefault=True), output_file=dict(argstr='--output %s', hash_files=False, name_source=['input_file'], name_template='%s_transformed.csv'), transforms=dict(argstr='%s', mandatory=True))
```

## Next Steps


---

*Source: test_auto_ApplyTransformsToPoints.py:6 | Complexity: Beginner | Last updated: 2026-05-18*