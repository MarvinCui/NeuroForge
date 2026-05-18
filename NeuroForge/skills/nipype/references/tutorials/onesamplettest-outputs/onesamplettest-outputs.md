# How To: Onesamplettest Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test OneSampleTTest outputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(beta_file=dict(extensions=None), bp_file=dict(extensions=None), dof_file=dict(extensions=None), error_file=dict(extensions=None), error_stddev_file=dict(extensions=None), error_var_file=dict(extensions=None), estimate_file=dict(extensions=None), frame_eigenvectors=dict(extensions=None), ftest_file=dict(), fwhm_file=dict(extensions=None), gamma_file=dict(), gamma_var_file=dict(), glm_dir=dict(), k2p_file=dict(extensions=None), mask_file=dict(extensions=None), sig_file=dict(), singular_values=dict(extensions=None), spatial_eigenvectors=dict(extensions=None), svd_stats_file=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(beta_file=dict(extensions=None), bp_file=dict(extensions=None), dof_file=dict(extensions=None), error_file=dict(extensions=None), error_stddev_file=dict(extensions=None), error_var_file=dict(extensions=None), estimate_file=dict(extensions=None), frame_eigenvectors=dict(extensions=None), ftest_file=dict(), fwhm_file=dict(extensions=None), gamma_file=dict(), gamma_var_file=dict(), glm_dir=dict(), k2p_file=dict(extensions=None), mask_file=dict(extensions=None), sig_file=dict(), singular_values=dict(extensions=None), spatial_eigenvectors=dict(extensions=None), svd_stats_file=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_OneSampleTTest.py:230 | Complexity: Beginner | Last updated: 2026-05-18*