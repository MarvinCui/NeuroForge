# How To: Ica Aroma Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ICA AROMA inputs

## Prerequisites

**Required Modules:**
- `aroma`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(TR=dict(argstr='-tr %.3f'), args=dict(argstr='%s'), denoise_type=dict(argstr='-den %s', mandatory=True, usedefault=True), dim=dict(argstr='-dim %d'), environ=dict(nohash=True, usedefault=True), feat_dir=dict(argstr='-feat %s', mandatory=True, xor=['in_file', 'mat_file', 'fnirt_warp_file', 'motion_parameters']), fnirt_warp_file=dict(argstr='-warp %s', extensions=None, xor=['feat_dir']), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, xor=['feat_dir']), mask=dict(argstr='-m %s', extensions=None, xor=['feat_dir']), mat_file=dict(argstr='-affmat %s', extensions=None, xor=['feat_dir']), melodic_dir=dict(argstr='-meldir %s'), motion_parameters=dict(argstr='-mc %s', extensions=None, mandatory=True, xor=['feat_dir']), out_dir=dict(argstr='-o %s', mandatory=True, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(TR=dict(argstr='-tr %.3f'), args=dict(argstr='%s'), denoise_type=dict(argstr='-den %s', mandatory=True, usedefault=True), dim=dict(argstr='-dim %d'), environ=dict(nohash=True, usedefault=True), feat_dir=dict(argstr='-feat %s', mandatory=True, xor=['in_file', 'mat_file', 'fnirt_warp_file', 'motion_parameters']), fnirt_warp_file=dict(argstr='-warp %s', extensions=None, xor=['feat_dir']), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, xor=['feat_dir']), mask=dict(argstr='-m %s', extensions=None, xor=['feat_dir']), mat_file=dict(argstr='-affmat %s', extensions=None, xor=['feat_dir']), melodic_dir=dict(argstr='-meldir %s'), motion_parameters=dict(argstr='-mc %s', extensions=None, mandatory=True, xor=['feat_dir']), out_dir=dict(argstr='-o %s', mandatory=True, usedefault=True))
```

## Next Steps


---

*Source: test_auto_ICA_AROMA.py:6 | Complexity: Beginner | Last updated: 2026-05-18*