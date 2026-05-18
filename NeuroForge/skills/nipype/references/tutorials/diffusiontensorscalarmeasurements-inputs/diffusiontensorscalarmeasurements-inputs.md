# How To: Diffusiontensorscalarmeasurements Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DiffusionTensorScalarMeasurements inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), enumeration=dict(argstr='--enumeration %s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-3), outputScalar=dict(argstr='%s', hash_files=False, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), enumeration=dict(argstr='--enumeration %s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-3), outputScalar=dict(argstr='%s', hash_files=False, position=-1))
```

## Next Steps


---

*Source: test_auto_DiffusionTensorScalarMeasurements.py:6 | Complexity: Beginner | Last updated: 2026-05-18*