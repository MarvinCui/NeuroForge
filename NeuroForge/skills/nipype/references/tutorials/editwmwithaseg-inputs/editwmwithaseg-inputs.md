# How To: Editwmwithaseg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EditWMwithAseg inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), brain_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), keep_in=dict(argstr='-keep-in'), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), seg_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), brain_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), keep_in=dict(argstr='-keep-in'), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), seg_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_EditWMwithAseg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*