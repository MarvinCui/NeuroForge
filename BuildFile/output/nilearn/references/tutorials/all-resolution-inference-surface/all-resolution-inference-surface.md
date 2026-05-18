# How To: All Resolution Inference Surface

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check cluster_level_inference that runs on each hemisphere.

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
# Fixtures: surf_img_1d, kwargs, expected_left, expected_right, expected_n_unique_values
```

## Step-by-Step Guide

### Step 1: 'Check cluster_level_inference that runs on each hemisphere.'

```python
'Check cluster_level_inference that runs on each hemisphere.'
```

**Verification:**
```python
assert np.sum(th_map.data.parts['left'] > 0) == expected_left
```

### Step 2: Assign data_left = _data_norm_isf(...)

```python
data_left = _data_norm_isf(surf_img_1d.data.parts['left'].shape)
```

**Verification:**
```python
assert len(np.unique(th_map.data.parts['left'])) == expected_n_unique_values
```

### Step 3: Assign unknown = 5.0

```python
data_left[2:4] = 5.0
```

**Verification:**
```python
assert np.sum(th_map.data.parts['right'] > 0) == expected_right
```

### Step 4: Assign data_right = _data_norm_isf(...)

```python
data_right = _data_norm_isf(surf_img_1d.data.parts['right'].shape)
```

**Verification:**
```python
assert len(np.unique(th_map.data.parts['right'])) == expected_n_unique_values
```

### Step 5: Assign unknown = 5.0

```python
data_right[2:5] = 5.0
```

### Step 6: Assign stat_img = new_img_like(...)

```python
stat_img = new_img_like(surf_img_1d, PolyData(left=data_left, right=data_right))
```

### Step 7: Assign th_map = cluster_level_inference(...)

```python
th_map = cluster_level_inference(stat_img, alpha=0.05, **kwargs)
```

**Verification:**
```python
assert np.sum(th_map.data.parts['left'] > 0) == expected_left
```


## Complete Example

```python
# Setup
# Fixtures: surf_img_1d, kwargs, expected_left, expected_right, expected_n_unique_values

# Workflow
'Check cluster_level_inference that runs on each hemisphere.'
data_left = _data_norm_isf(surf_img_1d.data.parts['left'].shape)
data_left[2:4] = 5.0
data_right = _data_norm_isf(surf_img_1d.data.parts['right'].shape)
data_right[2:5] = 5.0
stat_img = new_img_like(surf_img_1d, PolyData(left=data_left, right=data_right))
th_map = cluster_level_inference(stat_img, alpha=0.05, **kwargs)
assert np.sum(th_map.data.parts['left'] > 0) == expected_left
assert len(np.unique(th_map.data.parts['left'])) == expected_n_unique_values
assert np.sum(th_map.data.parts['right'] > 0) == expected_right
assert len(np.unique(th_map.data.parts['right'])) == expected_n_unique_values
```

## Next Steps


---

*Source: test_thresholding.py:320 | Complexity: Intermediate | Last updated: 2026-05-18*