# How To: Mriscalc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRIsCalc inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(action=dict(argstr='%s', mandatory=True, position=-2), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file1=dict(argstr='%s', extensions=None, mandatory=True, position=-3), in_file2=dict(argstr='%s', extensions=None, position=-1, xor=['in_float', 'in_int']), in_float=dict(argstr='%f', position=-1, xor=['in_file2', 'in_int']), in_int=dict(argstr='%d', position=-1, xor=['in_file2', 'in_float']), out_file=dict(argstr='-o %s', extensions=None, mandatory=True), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(action=dict(argstr='%s', mandatory=True, position=-2), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file1=dict(argstr='%s', extensions=None, mandatory=True, position=-3), in_file2=dict(argstr='%s', extensions=None, position=-1, xor=['in_float', 'in_int']), in_float=dict(argstr='%f', position=-1, xor=['in_file2', 'in_int']), in_int=dict(argstr='%d', position=-1, xor=['in_file2', 'in_float']), out_file=dict(argstr='-o %s', extensions=None, mandatory=True), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_MRIsCalc.py:6 | Complexity: Beginner | Last updated: 2026-05-18*