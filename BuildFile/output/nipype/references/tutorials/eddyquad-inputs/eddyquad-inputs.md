# How To: Eddyquad Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EddyQuad inputs

## Prerequisites

**Required Modules:**
- `epi`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), base_name=dict(argstr='%s', position=0, usedefault=True), bval_file=dict(argstr='--bvals %s', extensions=None, mandatory=True), bvec_file=dict(argstr='--bvecs %s', extensions=None), environ=dict(nohash=True, usedefault=True), field=dict(argstr='--field %s', extensions=None), idx_file=dict(argstr='--eddyIdx %s', extensions=None, mandatory=True), mask_file=dict(argstr='--mask %s', extensions=None, mandatory=True), output_dir=dict(argstr='--output-dir %s', name_source=['base_name'], name_template='%s.qc'), output_type=dict(), param_file=dict(argstr='--eddyParams %s', extensions=None, mandatory=True), slice_spec=dict(argstr='--slspec %s', extensions=None), verbose=dict(argstr='--verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), base_name=dict(argstr='%s', position=0, usedefault=True), bval_file=dict(argstr='--bvals %s', extensions=None, mandatory=True), bvec_file=dict(argstr='--bvecs %s', extensions=None), environ=dict(nohash=True, usedefault=True), field=dict(argstr='--field %s', extensions=None), idx_file=dict(argstr='--eddyIdx %s', extensions=None, mandatory=True), mask_file=dict(argstr='--mask %s', extensions=None, mandatory=True), output_dir=dict(argstr='--output-dir %s', name_source=['base_name'], name_template='%s.qc'), output_type=dict(), param_file=dict(argstr='--eddyParams %s', extensions=None, mandatory=True), slice_spec=dict(argstr='--slspec %s', extensions=None), verbose=dict(argstr='--verbose'))
```

## Next Steps


---

*Source: test_auto_EddyQuad.py:6 | Complexity: Beginner | Last updated: 2026-05-18*