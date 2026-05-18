# How To: Orientscalarvolume Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test OrientScalarVolume inputs

## Prerequisites

**Required Modules:**
- `converters`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume1=dict(argstr='%s', extensions=None, position=-2), orientation=dict(argstr='--orientation %s'), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume1=dict(argstr='%s', extensions=None, position=-2), orientation=dict(argstr='--orientation %s'), outputVolume=dict(argstr='%s', hash_files=False, position=-1))
```

## Next Steps


---

*Source: test_auto_OrientScalarVolume.py:6 | Complexity: Beginner | Last updated: 2026-05-18*