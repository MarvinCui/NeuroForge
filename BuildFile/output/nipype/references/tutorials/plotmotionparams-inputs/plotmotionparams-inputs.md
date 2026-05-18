# How To: Plotmotionparams Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test PlotMotionParams inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', mandatory=True, position=1), in_source=dict(mandatory=True), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), output_type=dict(), plot_size=dict(argstr='%s'), plot_type=dict(argstr='%s', mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', mandatory=True, position=1), in_source=dict(mandatory=True), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), output_type=dict(), plot_size=dict(argstr='%s'), plot_type=dict(argstr='%s', mandatory=True))
```

## Next Steps


---

*Source: test_auto_PlotMotionParams.py:6 | Complexity: Beginner | Last updated: 2026-05-18*