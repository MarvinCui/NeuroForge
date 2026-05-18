# How To: Segment Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Segment outputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(bias_corrected_image=dict(extensions=None), inverse_transformation_mat=dict(extensions=None), modulated_csf_image=dict(extensions=None), modulated_gm_image=dict(extensions=None), modulated_input_image=dict(deprecated='0.10', extensions=None, new_name='bias_corrected_image'), modulated_wm_image=dict(extensions=None), native_csf_image=dict(extensions=None), native_gm_image=dict(extensions=None), native_wm_image=dict(extensions=None), normalized_csf_image=dict(extensions=None), normalized_gm_image=dict(extensions=None), normalized_wm_image=dict(extensions=None), transformation_mat=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(bias_corrected_image=dict(extensions=None), inverse_transformation_mat=dict(extensions=None), modulated_csf_image=dict(extensions=None), modulated_gm_image=dict(extensions=None), modulated_input_image=dict(deprecated='0.10', extensions=None, new_name='bias_corrected_image'), modulated_wm_image=dict(extensions=None), native_csf_image=dict(extensions=None), native_gm_image=dict(extensions=None), native_wm_image=dict(extensions=None), normalized_csf_image=dict(extensions=None), normalized_gm_image=dict(extensions=None), normalized_wm_image=dict(extensions=None), transformation_mat=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_Segment.py:74 | Complexity: Beginner | Last updated: 2026-05-18*