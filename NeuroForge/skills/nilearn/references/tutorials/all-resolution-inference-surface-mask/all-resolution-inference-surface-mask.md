# How To: All Resolution Inference Surface Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check cluster_level_inference that runs on each hemisphere.

Here mask excludes the right hemisphere.

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
# Fixtures: surf_img_1d
```

## Step-by-Step Guide

### Step 1: 'Check cluster_level_inference that runs on each hemisphere.\n\n    Here mask excludes the right hemisphere.\n    '

```python
'Check cluster_level_inference that runs on each hemisphere.\n\n    Here mask excludes the right hemisphere.\n    '
```

**Verification:**
```python
assert np.sum(th_map.data.parts['left'] > 0) == 2
```

### Step 2: Assign data_left = _data_norm_isf(...)

```python
data_left = _data_norm_isf(surf_img_1d.data.parts['left'].shape)
```

**Verification:**
```python
assert np.sum(th_map.data.parts['right'] > 0) == 0
```

### Step 3: Assign unknown = 5.0

```python
data_left[2:4] = 5.0
```

### Step 4: Assign data_right = _data_norm_isf(...)

```python
data_right = _data_norm_isf(surf_img_1d.data.parts['right'].shape)
```

### Step 5: Assign unknown = 5.0

```python
data_right[2:5] = 5.0
```

### Step 6: Assign stat_img = new_img_like(...)

```python
stat_img = new_img_like(surf_img_1d, {'left': data_left, 'right': data_right})
```

### Step 7: Assign mask_left = np.ones(...)

```python
mask_left = np.ones(surf_img_1d.data.parts['left'].shape)
```

### Step 8: Assign mask_right = np.zeros(...)

```python
mask_right = np.zeros(surf_img_1d.data.parts['right'].shape)
```

### Step 9: Assign mask_img = new_img_like(...)

```python
mask_img = new_img_like(surf_img_1d, data={'left': mask_left, 'right': mask_right})
```

### Step 10: Assign th_map = cluster_level_inference(...)

```python
th_map = cluster_level_inference(stat_img, mask_img=mask_img, threshold=DEFAULT_Z_THRESHOLD, alpha=0.05)
```

**Verification:**
```python
assert np.sum(th_map.data.parts['left'] > 0) == 2
```


## Complete Example

```python
# Setup
# Fixtures: surf_img_1d

# Workflow
'Check cluster_level_inference that runs on each hemisphere.\n\n    Here mask excludes the right hemisphere.\n    '
data_left = _data_norm_isf(surf_img_1d.data.parts['left'].shape)
data_left[2:4] = 5.0
data_right = _data_norm_isf(surf_img_1d.data.parts['right'].shape)
data_right[2:5] = 5.0
stat_img = new_img_like(surf_img_1d, {'left': data_left, 'right': data_right})
mask_left = np.ones(surf_img_1d.data.parts['left'].shape)
mask_right = np.zeros(surf_img_1d.data.parts['right'].shape)
mask_img = new_img_like(surf_img_1d, data={'left': mask_left, 'right': mask_right})
th_map = cluster_level_inference(stat_img, mask_img=mask_img, threshold=DEFAULT_Z_THRESHOLD, alpha=0.05)
assert np.sum(th_map.data.parts['left'] > 0) == 2
assert np.sum(th_map.data.parts['right'] > 0) == 0
```

## Next Steps


---

*Source: test_thresholding.py:388 | Complexity: Advanced | Last updated: 2026-05-18*