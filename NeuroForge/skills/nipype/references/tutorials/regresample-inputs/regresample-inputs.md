# How To: Regresample Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RegResample inputs

## Prerequisites

**Required Modules:**
- `regutils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), flo_file=dict(argstr='-flo %s', extensions=None, mandatory=True), inter_val=dict(argstr='-inter %d'), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='%s', extensions=None, name_source=['flo_file'], name_template='%s', position=-1), pad_val=dict(argstr='-pad %f'), psf_alg=dict(argstr='-psf_alg %d'), psf_flag=dict(argstr='-psf'), ref_file=dict(argstr='-ref %s', extensions=None, mandatory=True), tensor_flag=dict(argstr='-tensor '), trans_file=dict(argstr='-trans %s', extensions=None), type=dict(argstr='-%s', position=-2, usedefault=True), verbosity_off_flag=dict(argstr='-voff'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), flo_file=dict(argstr='-flo %s', extensions=None, mandatory=True), inter_val=dict(argstr='-inter %d'), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='%s', extensions=None, name_source=['flo_file'], name_template='%s', position=-1), pad_val=dict(argstr='-pad %f'), psf_alg=dict(argstr='-psf_alg %d'), psf_flag=dict(argstr='-psf'), ref_file=dict(argstr='-ref %s', extensions=None, mandatory=True), tensor_flag=dict(argstr='-tensor '), trans_file=dict(argstr='-trans %s', extensions=None), type=dict(argstr='-%s', position=-2, usedefault=True), verbosity_off_flag=dict(argstr='-voff'))
```

## Next Steps


---

*Source: test_auto_RegResample.py:6 | Complexity: Beginner | Last updated: 2026-05-18*