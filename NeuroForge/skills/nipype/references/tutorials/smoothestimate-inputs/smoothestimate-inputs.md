# How To: Smoothestimate Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SmoothEstimate inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dof=dict(argstr='--dof=%d', mandatory=True, xor=['zstat_file']), environ=dict(nohash=True, usedefault=True), mask_file=dict(argstr='--mask=%s', extensions=None, mandatory=True), output_type=dict(), residual_fit_file=dict(argstr='--res=%s', extensions=None, requires=['dof']), zstat_file=dict(argstr='--zstat=%s', extensions=None, xor=['dof']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dof=dict(argstr='--dof=%d', mandatory=True, xor=['zstat_file']), environ=dict(nohash=True, usedefault=True), mask_file=dict(argstr='--mask=%s', extensions=None, mandatory=True), output_type=dict(), residual_fit_file=dict(argstr='--res=%s', extensions=None, requires=['dof']), zstat_file=dict(argstr='--zstat=%s', extensions=None, xor=['dof']))
```

## Next Steps


---

*Source: test_auto_SmoothEstimate.py:6 | Complexity: Beginner | Last updated: 2026-05-18*