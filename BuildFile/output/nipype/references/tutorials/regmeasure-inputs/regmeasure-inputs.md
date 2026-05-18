# How To: Regmeasure Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RegMeasure inputs

## Prerequisites

**Required Modules:**
- `regutils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), flo_file=dict(argstr='-flo %s', extensions=None, mandatory=True), measure_type=dict(argstr='-%s', mandatory=True), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='-out %s', extensions=None, name_source=['flo_file'], name_template='%s'), ref_file=dict(argstr='-ref %s', extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), flo_file=dict(argstr='-flo %s', extensions=None, mandatory=True), measure_type=dict(argstr='-%s', mandatory=True), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='-out %s', extensions=None, name_source=['flo_file'], name_template='%s'), ref_file=dict(argstr='-ref %s', extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_RegMeasure.py:6 | Complexity: Beginner | Last updated: 2026-05-18*