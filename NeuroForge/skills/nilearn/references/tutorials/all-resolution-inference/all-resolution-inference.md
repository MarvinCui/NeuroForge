# How To: All Resolution Inference

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test all resolution inference

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
# Fixtures: data_norm_isf, affine_eye, kwargs, expected, expected_n_unique_values
```

## Step-by-Step Guide

### Step 1: Assign data = data_norm_isf

```python
data = data_norm_isf
```

**Verification:**
```python
assert np.sum(vals > 0) == expected
```

### Step 2: Assign unknown = 5.0

```python
data[2:4, 5:7, 6:8] = 5.0
```

**Verification:**
```python
assert len(np.unique(vals)) == expected_n_unique_values
```

### Step 3: Assign stat_img = Nifti1Image(...)

```python
stat_img = Nifti1Image(data, affine_eye)
```

### Step 4: Assign th_map = cluster_level_inference(...)

```python
th_map = cluster_level_inference(stat_img, alpha=0.05, **kwargs)
```

### Step 5: Assign vals = get_data(...)

```python
vals = get_data(th_map)
```

**Verification:**
```python
assert np.sum(vals > 0) == expected
```


## Complete Example

```python
# Setup
# Fixtures: data_norm_isf, affine_eye, kwargs, expected, expected_n_unique_values

# Workflow
data = data_norm_isf
data[2:4, 5:7, 6:8] = 5.0
stat_img = Nifti1Image(data, affine_eye)
th_map = cluster_level_inference(stat_img, alpha=0.05, **kwargs)
vals = get_data(th_map)
assert np.sum(vals > 0) == expected
assert len(np.unique(vals)) == expected_n_unique_values
```

## Next Steps


---

*Source: test_thresholding.py:291 | Complexity: Intermediate | Last updated: 2026-05-18*