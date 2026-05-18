# How To: Sphere Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Sphere inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), in_smoothwm=dict(copyfile=True, extensions=None), magic=dict(argstr='-q'), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s.sphere', position=-1), seed=dict(argstr='-seed %d'), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), in_smoothwm=dict(copyfile=True, extensions=None), magic=dict(argstr='-q'), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s.sphere', position=-1), seed=dict(argstr='-seed %d'), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_Sphere.py:6 | Complexity: Beginner | Last updated: 2026-05-18*