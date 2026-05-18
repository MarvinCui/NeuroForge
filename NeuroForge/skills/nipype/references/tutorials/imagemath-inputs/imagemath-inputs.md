# How To: Imagemath Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ImageMath inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s', position=-1), copy_header=dict(usedefault=True), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), op1=dict(argstr='%s', extensions=None, mandatory=True, position=-3), op2=dict(argstr='%s', position=-2), operation=dict(argstr='%s', mandatory=True, position=3), output_image=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['op1'], name_template='%s_maths', position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s', position=-1), copy_header=dict(usedefault=True), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), op1=dict(argstr='%s', extensions=None, mandatory=True, position=-3), op2=dict(argstr='%s', position=-2), operation=dict(argstr='%s', mandatory=True, position=3), output_image=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['op1'], name_template='%s_maths', position=2))
```

## Next Steps


---

*Source: test_auto_ImageMath.py:6 | Complexity: Beginner | Last updated: 2026-05-18*