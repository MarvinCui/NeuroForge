# How To: Labelconvert Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test LabelConvert inputs

## Prerequisites

**Required Modules:**
- `connectivity`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_config=dict(argstr='%s', extensions=None, position=-2), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), in_lut=dict(argstr='%s', extensions=None, mandatory=True, position=-3), num_threads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), spine=dict(argstr='-spine %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_config=dict(argstr='%s', extensions=None, position=-2), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), in_lut=dict(argstr='%s', extensions=None, mandatory=True, position=-3), num_threads=dict(argstr='-nthreads %d', nohash=True), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), spine=dict(argstr='-spine %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_LabelConvert.py:6 | Complexity: Beginner | Last updated: 2026-05-18*