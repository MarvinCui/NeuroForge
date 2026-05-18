# How To: Grayscalemodelmaker Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GrayscaleModelMaker inputs

## Prerequisites

**Required Modules:**
- `surface`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputGeometry=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), decimate=dict(argstr='--decimate %f'), environ=dict(nohash=True, usedefault=True), name=dict(argstr='--name %s'), pointnormals=dict(argstr='--pointnormals '), smooth=dict(argstr='--smooth %d'), splitnormals=dict(argstr='--splitnormals '), threshold=dict(argstr='--threshold %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputGeometry=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), decimate=dict(argstr='--decimate %f'), environ=dict(nohash=True, usedefault=True), name=dict(argstr='--name %s'), pointnormals=dict(argstr='--pointnormals '), smooth=dict(argstr='--smooth %d'), splitnormals=dict(argstr='--splitnormals '), threshold=dict(argstr='--threshold %f'))
```

## Next Steps


---

*Source: test_auto_GrayscaleModelMaker.py:6 | Complexity: Beginner | Last updated: 2026-05-18*