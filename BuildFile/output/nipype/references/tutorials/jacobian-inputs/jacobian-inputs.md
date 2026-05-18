# How To: Jacobian Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Jacobian inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_mappedsurf=dict(argstr='%s', extensions=None, mandatory=True, position=-2), in_origsurf=dict(argstr='%s', extensions=None, mandatory=True, position=-3), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_origsurf'], name_template='%s.jacobian', position=-1), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_mappedsurf=dict(argstr='%s', extensions=None, mandatory=True, position=-2), in_origsurf=dict(argstr='%s', extensions=None, mandatory=True, position=-3), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_origsurf'], name_template='%s.jacobian', position=-1), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_Jacobian.py:6 | Complexity: Beginner | Last updated: 2026-05-18*