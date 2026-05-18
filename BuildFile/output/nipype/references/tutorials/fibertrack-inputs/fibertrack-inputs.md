# How To: Fibertrack Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test fibertrack inputs

## Prerequisites

**Required Modules:**
- `fibertrack`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), forbidden_label=dict(argstr='--forbidden_label %d'), force=dict(argstr='--force '), input_roi_file=dict(argstr='--input_roi_file %s', extensions=None), input_tensor_file=dict(argstr='--input_tensor_file %s', extensions=None), max_angle=dict(argstr='--max_angle %f'), min_fa=dict(argstr='--min_fa %f'), output_fiber_file=dict(argstr='--output_fiber_file %s', hash_files=False), really_verbose=dict(argstr='--really_verbose '), source_label=dict(argstr='--source_label %d'), step_size=dict(argstr='--step_size %f'), target_label=dict(argstr='--target_label %d'), verbose=dict(argstr='--verbose '), whole_brain=dict(argstr='--whole_brain '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), forbidden_label=dict(argstr='--forbidden_label %d'), force=dict(argstr='--force '), input_roi_file=dict(argstr='--input_roi_file %s', extensions=None), input_tensor_file=dict(argstr='--input_tensor_file %s', extensions=None), max_angle=dict(argstr='--max_angle %f'), min_fa=dict(argstr='--min_fa %f'), output_fiber_file=dict(argstr='--output_fiber_file %s', hash_files=False), really_verbose=dict(argstr='--really_verbose '), source_label=dict(argstr='--source_label %d'), step_size=dict(argstr='--step_size %f'), target_label=dict(argstr='--target_label %d'), verbose=dict(argstr='--verbose '), whole_brain=dict(argstr='--whole_brain '))
```

## Next Steps


---

*Source: test_auto_fibertrack.py:6 | Complexity: Beginner | Last updated: 2026-05-18*