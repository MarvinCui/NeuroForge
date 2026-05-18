# How To: All Resolution Inference One Sided

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test all resolution inference one sided

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy.stats`
- `nilearn.datasets`
- `nilearn.exceptions`
- `nilearn.glm`
- `nilearn.glm.thresholding`
- `nilearn.image`
- `nilearn.surface.surface`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: data_norm_isf, img_3d_ones_eye, affine_eye
```

## Step-by-Step Guide

### Step 1: Assign data = data_norm_isf

```python
data = data_norm_isf
```

**Verification:**
```python
assert_equal(z_th, norm.isf(0.001))
```

### Step 2: Assign unknown = 5.0

```python
data[2:4, 5:7, 6:8] = 5.0
```

### Step 3: Assign stat_img = Nifti1Image(...)

```python
stat_img = Nifti1Image(data, affine_eye)
```

### Step 4: Assign unknown = threshold_stats_img(...)

```python
_, z_th = threshold_stats_img(stat_img, mask_img=img_3d_ones_eye, alpha=0.001, height_control='fpr', cluster_threshold=10, two_sided=False)
```

### Step 5: Call assert_equal()

```python
assert_equal(z_th, norm.isf(0.001))
```


## Complete Example

```python
# Setup
# Fixtures: data_norm_isf, img_3d_ones_eye, affine_eye

# Workflow
data = data_norm_isf
data[2:4, 5:7, 6:8] = 5.0
stat_img = Nifti1Image(data, affine_eye)
_, z_th = threshold_stats_img(stat_img, mask_img=img_3d_ones_eye, alpha=0.001, height_control='fpr', cluster_threshold=10, two_sided=False)
assert_equal(z_th, norm.isf(0.001))
```

## Next Steps


---

*Source: test_thresholding.py:429 | Complexity: Intermediate | Last updated: 2026-05-18*