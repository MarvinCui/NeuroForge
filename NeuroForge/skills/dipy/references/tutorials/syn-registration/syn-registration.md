# How To: Syn Registration

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate syn_registration: test syn registration

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.align`
- `dipy.align.imwarp`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.utils`


## Step-by-Step Guide

### Step 1: Assign unknown = syn_registration(...)

```python
warped_moving, mapping = syn_registration(subset_b0, subset_t2, moving_affine=hardi_affine, static_affine=MNI_T2_affine, step_length=0.1, metric='CC', dim=3, level_iters=[5, 5, 5], sigma_diff=2.0, radius=1, prealign=None)
```


## Complete Example

```python
# Workflow
warped_moving, mapping = syn_registration(subset_b0, subset_t2, moving_affine=hardi_affine, static_affine=MNI_T2_affine, step_length=0.1, metric='CC', dim=3, level_iters=[5, 5, 5], sigma_diff=2.0, radius=1, prealign=None)
```

## Next Steps


---

*Source: test_api.py:66 | Complexity: Beginner | Last updated: 2026-05-18*