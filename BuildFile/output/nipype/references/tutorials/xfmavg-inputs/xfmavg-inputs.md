# How To: Xfmavg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test XfmAvg inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), avg_linear=dict(argstr='-avg_linear'), avg_nonlinear=dict(argstr='-avg_nonlinear'), clobber=dict(argstr='-clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), ignore_linear=dict(argstr='-ignore_linear'), ignore_nonlinear=dict(argstr='-ignore_nonline'), input_files=dict(argstr='%s', mandatory=True, position=-2, sep=' '), input_grid_files=dict(), output_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), verbose=dict(argstr='-verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), avg_linear=dict(argstr='-avg_linear'), avg_nonlinear=dict(argstr='-avg_nonlinear'), clobber=dict(argstr='-clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), ignore_linear=dict(argstr='-ignore_linear'), ignore_nonlinear=dict(argstr='-ignore_nonline'), input_files=dict(argstr='%s', mandatory=True, position=-2, sep=' '), input_grid_files=dict(), output_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), verbose=dict(argstr='-verbose'))
```

## Next Steps


---

*Source: test_auto_XfmAvg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*