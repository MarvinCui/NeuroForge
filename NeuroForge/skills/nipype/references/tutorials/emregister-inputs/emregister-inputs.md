# How To: Emregister Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EMRegister inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), mask=dict(argstr='-mask %s', extensions=None), nbrspacing=dict(argstr='-uns %d'), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_file'], name_template='%s_transform.lta', position=-1), skull=dict(argstr='-skull'), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, mandatory=True, position=-2), transform=dict(argstr='-t %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), mask=dict(argstr='-mask %s', extensions=None), nbrspacing=dict(argstr='-uns %d'), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_file'], name_template='%s_transform.lta', position=-1), skull=dict(argstr='-skull'), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, mandatory=True, position=-2), transform=dict(argstr='-t %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_EMRegister.py:6 | Complexity: Beginner | Last updated: 2026-05-18*