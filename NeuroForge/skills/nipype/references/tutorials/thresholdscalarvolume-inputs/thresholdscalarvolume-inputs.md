# How To: Thresholdscalarvolume Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ThresholdScalarVolume inputs

## Prerequisites

**Required Modules:**
- `thresholdscalarvolume`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), lower=dict(argstr='--lower %d'), outsidevalue=dict(argstr='--outsidevalue %d'), threshold=dict(argstr='--threshold %d'), thresholdtype=dict(argstr='--thresholdtype %s'), upper=dict(argstr='--upper %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputVolume=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), lower=dict(argstr='--lower %d'), outsidevalue=dict(argstr='--outsidevalue %d'), threshold=dict(argstr='--threshold %d'), thresholdtype=dict(argstr='--thresholdtype %s'), upper=dict(argstr='--upper %d'))
```

## Next Steps


---

*Source: test_auto_ThresholdScalarVolume.py:6 | Complexity: Beginner | Last updated: 2026-05-18*