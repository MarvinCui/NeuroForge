# How To: Estimatemodel Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EstimateModel outputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(ARcoef=dict(), Cbetas=dict(), RPVimage=dict(extensions=['.hdr', '.img', '.img.gz', '.nii']), SDbetas=dict(), SDerror=dict(), beta_images=dict(), con_images=dict(), ess_images=dict(), labels=dict(extensions=['.hdr', '.img', '.img.gz', '.nii']), mask_image=dict(extensions=['.hdr', '.img', '.img.gz', '.nii']), residual_image=dict(extensions=['.hdr', '.img', '.img.gz', '.nii']), residual_images=dict(), spmF_images=dict(), spmT_images=dict(), spm_mat_file=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(ARcoef=dict(), Cbetas=dict(), RPVimage=dict(extensions=['.hdr', '.img', '.img.gz', '.nii']), SDbetas=dict(), SDerror=dict(), beta_images=dict(), con_images=dict(), ess_images=dict(), labels=dict(extensions=['.hdr', '.img', '.img.gz', '.nii']), mask_image=dict(extensions=['.hdr', '.img', '.img.gz', '.nii']), residual_image=dict(extensions=['.hdr', '.img', '.img.gz', '.nii']), residual_images=dict(), spmF_images=dict(), spmT_images=dict(), spm_mat_file=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_EstimateModel.py:40 | Complexity: Beginner | Last updated: 2026-05-18*