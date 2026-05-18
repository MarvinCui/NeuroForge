# How To: Caregister Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CARegister inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(A=dict(argstr='-A %d'), align=dict(argstr='-align-%s'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), invert_and_save=dict(argstr='-invert-and-save', position=-4), l_files=dict(argstr='-l %s'), levels=dict(argstr='-levels %d'), mask=dict(argstr='-mask %s', extensions=None), no_big_ventricles=dict(argstr='-nobigventricles'), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, position=-2), transform=dict(argstr='-T %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(A=dict(argstr='-A %d'), align=dict(argstr='-align-%s'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), invert_and_save=dict(argstr='-invert-and-save', position=-4), l_files=dict(argstr='-l %s'), levels=dict(argstr='-levels %d'), mask=dict(argstr='-mask %s', extensions=None), no_big_ventricles=dict(argstr='-nobigventricles'), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, position=-2), transform=dict(argstr='-T %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_CARegister.py:6 | Complexity: Beginner | Last updated: 2026-05-18*