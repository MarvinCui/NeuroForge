# How To: Multiplyscalarvolumes Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MultiplyScalarVolumes inputs

## Prerequisites

**Required Modules:**
- `arithmetic`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume1=dict(argstr='%s', extensions=None, position=-3), inputVolume2=dict(argstr='%s', extensions=None, position=-2), order=dict(argstr='--order %s'), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume1=dict(argstr='%s', extensions=None, position=-3), inputVolume2=dict(argstr='%s', extensions=None, position=-2), order=dict(argstr='--order %s'), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```

## Next Steps


---

*Source: test_auto_MultiplyScalarVolumes.py:6 | Complexity: Beginner | Last updated: 2026-05-18*