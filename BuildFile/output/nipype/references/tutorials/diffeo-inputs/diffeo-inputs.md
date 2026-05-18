# How To: Diffeo Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Diffeo inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixed_file=dict(argstr='%s', extensions=None, position=0), ftol=dict(argstr='%g', mandatory=True, position=5, usedefault=True), legacy=dict(argstr='%d', mandatory=True, position=3, usedefault=True), mask_file=dict(argstr='%s', extensions=None, position=2), moving_file=dict(argstr='%s', copyfile=False, extensions=None, position=1), n_iters=dict(argstr='%d', mandatory=True, position=4, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixed_file=dict(argstr='%s', extensions=None, position=0), ftol=dict(argstr='%g', mandatory=True, position=5, usedefault=True), legacy=dict(argstr='%d', mandatory=True, position=3, usedefault=True), mask_file=dict(argstr='%s', extensions=None, position=2), moving_file=dict(argstr='%s', copyfile=False, extensions=None, position=1), n_iters=dict(argstr='%d', mandatory=True, position=4, usedefault=True))
```

## Next Steps


---

*Source: test_auto_Diffeo.py:6 | Complexity: Beginner | Last updated: 2026-05-18*