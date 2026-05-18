# How To: Threshold Stats Img

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test threshold stats img

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
assert np.sum(vals > 0) == 8
```

### Step 2: Assign unknown = 5.0

```python
data[2:4, 5:7, 6:8] = 5.0
```

**Verification:**
```python
assert np.sum(vals > 0) == 0
```

### Step 3: Assign stat_img = Nifti1Image(...)

```python
stat_img = Nifti1Image(data, affine_eye)
```

**Verification:**
```python
assert z_th == norm.isf(0.0005)
```

### Step 4: Assign unknown = threshold_stats_img(...)

```python
th_map, _ = threshold_stats_img(stat_img, mask_img=img_3d_ones_eye, alpha=0.001, height_control='fpr', cluster_threshold=0)
```

**Verification:**
```python
assert np.sum(vals > 0) == 8
```

### Step 5: Assign vals = get_data(...)

```python
vals = get_data(th_map)
```

**Verification:**
```python
assert threshold > 1.64
```

### Step 6: Assign unknown = threshold_stats_img(...)

```python
th_map, z_th = threshold_stats_img(stat_img, mask_img=img_3d_ones_eye, alpha=0.001, height_control='fpr', cluster_threshold=10)
```

**Verification:**
```python
assert th_map is None
```

### Step 7: Assign vals = get_data(...)

```python
vals = get_data(th_map)
```

**Verification:**
```python
assert np.sum(vals > 0) == 0
```

### Step 8: Assign unknown = threshold_stats_img(...)

```python
th_map, threshold = threshold_stats_img(None, None, alpha=0.05, height_control='fpr', cluster_threshold=0)
```

**Verification:**
```python
assert threshold > 1.64
```

### Step 9: Assign unknown = threshold_stats_img(...)

```python
th_map, _ = threshold_stats_img(stat_img, mask_img=img_3d_ones_eye, alpha=0.05, height_control=control, cluster_threshold=5)
```

### Step 10: Assign vals = get_data(...)

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
# Fixtures: data_norm_isf, img_3d_ones_eye, affine_eye

# Workflow
data = data_norm_isf
data[2:4, 5:7, 6:8] = 5.0
stat_img = Nifti1Image(data, affine_eye)
th_map, _ = threshold_stats_img(stat_img, mask_img=img_3d_ones_eye, alpha=0.001, height_control='fpr', cluster_threshold=0)
vals = get_data(th_map)
assert np.sum(vals > 0) == 8
th_map, z_th = threshold_stats_img(stat_img, mask_img=img_3d_ones_eye, alpha=0.001, height_control='fpr', cluster_threshold=10)
vals = get_data(th_map)
assert np.sum(vals > 0) == 0
assert z_th == norm.isf(0.0005)
for control in ['fdr', 'bonferroni']:
    th_map, _ = threshold_stats_img(stat_img, mask_img=img_3d_ones_eye, alpha=0.05, height_control=control, cluster_threshold=5)
    vals = get_data(th_map)
    assert np.sum(vals > 0) == 8
th_map, threshold = threshold_stats_img(None, None, alpha=0.05, height_control='fpr', cluster_threshold=0)
assert threshold > 1.64
assert th_map is None
```

## Next Steps


---

*Source: test_thresholding.py:172 | Complexity: Advanced | Last updated: 2026-05-18*