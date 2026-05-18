# How To: Avscale Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AvScale inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(all_param=dict(argstr='--allparams'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), mat_file=dict(argstr='%s', extensions=None, position=-2), ref_file=dict(argstr='%s', extensions=None, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(all_param=dict(argstr='--allparams'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), mat_file=dict(argstr='%s', extensions=None, position=-2), ref_file=dict(argstr='%s', extensions=None, position=-1))
```

## Next Steps


---

*Source: test_auto_AvScale.py:6 | Complexity: Beginner | Last updated: 2026-05-18*