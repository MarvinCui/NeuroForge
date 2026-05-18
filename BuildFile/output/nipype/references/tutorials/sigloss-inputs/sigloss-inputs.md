# How To: Sigloss Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SigLoss inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), echo_time=dict(argstr='--te=%f'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), mask_file=dict(argstr='-m %s', extensions=None), out_file=dict(argstr='-s %s', extensions=None, genfile=True), output_type=dict(), slice_direction=dict(argstr='-d %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), echo_time=dict(argstr='--te=%f'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), mask_file=dict(argstr='-m %s', extensions=None), out_file=dict(argstr='-s %s', extensions=None, genfile=True), output_type=dict(), slice_direction=dict(argstr='-d %s'))
```

## Next Steps


---

*Source: test_auto_SigLoss.py:6 | Complexity: Beginner | Last updated: 2026-05-18*