# How To: Vbmsegment Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test VBMSegment outputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(bias_corrected_images=dict(), dartel_input_images=dict(), forward_deformation_field=dict(), inverse_deformation_field=dict(), jacobian_determinant_images=dict(), modulated_class_images=dict(), native_class_images=dict(), normalized_bias_corrected_images=dict(), normalized_class_images=dict(), pve_label_native_images=dict(), pve_label_normalized_images=dict(), pve_label_registered_images=dict(), transformation_mat=dict())
```


## Complete Example

```python
# Workflow
output_map = dict(bias_corrected_images=dict(), dartel_input_images=dict(), forward_deformation_field=dict(), inverse_deformation_field=dict(), jacobian_determinant_images=dict(), modulated_class_images=dict(), native_class_images=dict(), normalized_bias_corrected_images=dict(), normalized_class_images=dict(), pve_label_native_images=dict(), pve_label_normalized_images=dict(), pve_label_registered_images=dict(), transformation_mat=dict())
```

## Next Steps


---

*Source: test_auto_VBMSegment.py:157 | Complexity: Beginner | Last updated: 2026-05-18*