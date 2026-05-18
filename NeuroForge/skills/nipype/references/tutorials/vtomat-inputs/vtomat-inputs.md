# How To: Vtomat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test VtoMat inputs

## Prerequisites

**Required Modules:**
- `vista`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-in %s', extensions=None, mandatory=True, position=1), out_file=dict(argstr='-out %s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_file'], name_template='%s.mat', position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-in %s', extensions=None, mandatory=True, position=1), out_file=dict(argstr='-out %s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_file'], name_template='%s.mat', position=-1))
```

## Next Steps


---

*Source: test_auto_VtoMat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*