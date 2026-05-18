# How To: Robusttemplate Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RobustTemplate inputs

## Prerequisites

**Required Modules:**
- `longitudinal`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), auto_detect_sensitivity=dict(argstr='--satit', mandatory=True, xor=['outlier_sensitivity']), average_metric=dict(argstr='--average %d'), environ=dict(nohash=True, usedefault=True), fixed_timepoint=dict(argstr='--fixtp'), in_files=dict(argstr='--mov %s', mandatory=True), in_intensity_scales=dict(argstr='--iscalein %s'), initial_timepoint=dict(argstr='--inittp %d'), initial_transforms=dict(argstr='--ixforms %s'), intensity_scaling=dict(argstr='--iscale'), no_iteration=dict(argstr='--noit'), num_threads=dict(), out_file=dict(argstr='--template %s', extensions=None, mandatory=True, usedefault=True), outlier_sensitivity=dict(argstr='--sat %.4f', mandatory=True, xor=['auto_detect_sensitivity']), scaled_intensity_outputs=dict(argstr='--iscaleout %s'), subjects_dir=dict(), subsample_threshold=dict(argstr='--subsample %d'), transform_outputs=dict(argstr='--lta %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), auto_detect_sensitivity=dict(argstr='--satit', mandatory=True, xor=['outlier_sensitivity']), average_metric=dict(argstr='--average %d'), environ=dict(nohash=True, usedefault=True), fixed_timepoint=dict(argstr='--fixtp'), in_files=dict(argstr='--mov %s', mandatory=True), in_intensity_scales=dict(argstr='--iscalein %s'), initial_timepoint=dict(argstr='--inittp %d'), initial_transforms=dict(argstr='--ixforms %s'), intensity_scaling=dict(argstr='--iscale'), no_iteration=dict(argstr='--noit'), num_threads=dict(), out_file=dict(argstr='--template %s', extensions=None, mandatory=True, usedefault=True), outlier_sensitivity=dict(argstr='--sat %.4f', mandatory=True, xor=['auto_detect_sensitivity']), scaled_intensity_outputs=dict(argstr='--iscaleout %s'), subjects_dir=dict(), subsample_threshold=dict(argstr='--subsample %d'), transform_outputs=dict(argstr='--lta %s'))
```

## Next Steps


---

*Source: test_auto_RobustTemplate.py:6 | Complexity: Beginner | Last updated: 2026-05-18*