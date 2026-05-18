# How To: Eddy Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Eddy outputs

## Prerequisites

**Required Modules:**
- `epi`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(out_cnr_maps=dict(extensions=None), out_corrected=dict(extensions=None), out_movement_over_time=dict(extensions=None), out_movement_rms=dict(extensions=None), out_outlier_free=dict(extensions=None), out_outlier_map=dict(extensions=None), out_outlier_n_sqr_stdev_map=dict(extensions=None), out_outlier_n_stdev_map=dict(extensions=None), out_outlier_report=dict(extensions=None), out_parameter=dict(extensions=None), out_residuals=dict(extensions=None), out_restricted_movement_rms=dict(extensions=None), out_rotated_bvecs=dict(extensions=None), out_shell_alignment_parameters=dict(extensions=None), out_shell_pe_translation_parameters=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(out_cnr_maps=dict(extensions=None), out_corrected=dict(extensions=None), out_movement_over_time=dict(extensions=None), out_movement_rms=dict(extensions=None), out_outlier_free=dict(extensions=None), out_outlier_map=dict(extensions=None), out_outlier_n_sqr_stdev_map=dict(extensions=None), out_outlier_n_stdev_map=dict(extensions=None), out_outlier_report=dict(extensions=None), out_parameter=dict(extensions=None), out_residuals=dict(extensions=None), out_restricted_movement_rms=dict(extensions=None), out_rotated_bvecs=dict(extensions=None), out_shell_alignment_parameters=dict(extensions=None), out_shell_pe_translation_parameters=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_Eddy.py:227 | Complexity: Beginner | Last updated: 2026-05-18*