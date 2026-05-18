# How To: All Resolution Inference With Mask

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test all resolution inference with mask

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
# Fixtures: img_3d_ones_eye, affine_eye, data_norm_isf
```

## Step-by-Step Guide

### Step 1: Assign data = data_norm_isf

```python
data = data_norm_isf
```

**Verification:**
```python
assert np.sum(vals > 0) == 8
```

### Step 2: Assign unknown = 5.0

```python
data[2:4, 5:7, 6:8] = 5.0
```

### Step 3: Assign stat_img = Nifti1Image(...)

```python
stat_img = Nifti1Image(data, affine_eye)
```

### Step 4: Assign th_map = cluster_level_inference(...)

```python
th_map = cluster_level_inference(stat_img, mask_img=img_3d_ones_eye, threshold=DEFAULT_Z_THRESHOLD, alpha=0.05)
```

### Step 5: Assign vals = get_data(...)

```python
vals = get_data(th_map)
```

**Verification:**
```python
assert np.sum(vals > 0) == 8
```


## Complete Example

```python
# Setup
# Fixtures: img_3d_ones_eye, affine_eye, data_norm_isf

# Workflow
data = data_norm_isf
data[2:4, 5:7, 6:8] = 5.0
stat_img = Nifti1Image(data, affine_eye)
th_map = cluster_level_inference(stat_img, mask_img=img_3d_ones_eye, threshold=DEFAULT_Z_THRESHOLD, alpha=0.05)
vals = get_data(th_map)
assert np.sum(vals > 0) == 8
```

## Next Steps


---

*Source: test_thresholding.py:351 | Complexity: Intermediate | Last updated: 2026-05-18*