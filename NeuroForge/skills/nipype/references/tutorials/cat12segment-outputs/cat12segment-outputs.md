# How To: Cat12Segment Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CAT12Segment outputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(bias_corrected_image=dict(extensions=None), csf_dartel_image=dict(extensions=None), csf_modulated_image=dict(extensions=None), csf_native_image=dict(extensions=None), gm_dartel_image=dict(extensions=None), gm_modulated_image=dict(extensions=None), gm_native_image=dict(extensions=None), label_files=dict(), label_roi=dict(extensions=None), label_rois=dict(extensions=None), lh_central_surface=dict(extensions=None), lh_sphere_surface=dict(extensions=None), mri_images=dict(), report=dict(extensions=None), report_files=dict(), rh_central_surface=dict(extensions=None), rh_sphere_surface=dict(extensions=None), surface_files=dict(), wm_dartel_image=dict(extensions=None), wm_modulated_image=dict(extensions=None), wm_native_image=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(bias_corrected_image=dict(extensions=None), csf_dartel_image=dict(extensions=None), csf_modulated_image=dict(extensions=None), csf_native_image=dict(extensions=None), gm_dartel_image=dict(extensions=None), gm_modulated_image=dict(extensions=None), gm_native_image=dict(extensions=None), label_files=dict(), label_roi=dict(extensions=None), label_rois=dict(extensions=None), lh_central_surface=dict(extensions=None), lh_sphere_surface=dict(extensions=None), mri_images=dict(), report=dict(extensions=None), report_files=dict(), rh_central_surface=dict(extensions=None), rh_sphere_surface=dict(extensions=None), surface_files=dict(), wm_dartel_image=dict(extensions=None), wm_modulated_image=dict(extensions=None), wm_native_image=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_CAT12Segment.py:216 | Complexity: Beginner | Last updated: 2026-05-18*