# How To: Regjacobian Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RegJacobian inputs

## Prerequisites

**Required Modules:**
- `regutils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='%s', extensions=None, name_source=['trans_file'], name_template='%s', position=-1), ref_file=dict(argstr='-ref %s', extensions=None), trans_file=dict(argstr='-trans %s', extensions=None, mandatory=True), type=dict(argstr='-%s', position=-2, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='%s', extensions=None, name_source=['trans_file'], name_template='%s', position=-1), ref_file=dict(argstr='-ref %s', extensions=None), trans_file=dict(argstr='-trans %s', extensions=None, mandatory=True), type=dict(argstr='-%s', position=-2, usedefault=True))
```

## Next Steps


---

*Source: test_auto_RegJacobian.py:6 | Complexity: Beginner | Last updated: 2026-05-18*