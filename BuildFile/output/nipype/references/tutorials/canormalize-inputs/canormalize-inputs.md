# How To: Canormalize Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CANormalize inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), atlas=dict(argstr='%s', extensions=None, mandatory=True, position=-3), control_points=dict(argstr='-c %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), long_file=dict(argstr='-long %s', extensions=None), mask=dict(argstr='-mask %s', extensions=None), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_norm', position=-1), subjects_dir=dict(), transform=dict(argstr='%s', extensions=None, mandatory=True, position=-2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), atlas=dict(argstr='%s', extensions=None, mandatory=True, position=-3), control_points=dict(argstr='-c %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), long_file=dict(argstr='-long %s', extensions=None), mask=dict(argstr='-mask %s', extensions=None), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_norm', position=-1), subjects_dir=dict(), transform=dict(argstr='%s', extensions=None, mandatory=True, position=-2))
```

## Next Steps


---

*Source: test_auto_CANormalize.py:6 | Complexity: Beginner | Last updated: 2026-05-18*