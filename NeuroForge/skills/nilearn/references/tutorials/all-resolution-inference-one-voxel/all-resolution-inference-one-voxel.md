# How To: All Resolution Inference One Voxel

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test all resolution inference one voxel

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
# Fixtures: data_norm_isf, affine_eye
```

## Step-by-Step Guide

### Step 1: Assign data = data_norm_isf

```python
data = data_norm_isf
```

**Verification:**
```python
assert np.sum(vals > 0) == 1
```

### Step 2: Assign unknown = 10

```python
data[3, 6, 7] = 10
```

### Step 3: Assign stat_img = Nifti1Image(...)

```python
stat_img = Nifti1Image(data, affine_eye)
```

### Step 4: Assign th_map = cluster_level_inference(...)

```python
th_map = cluster_level_inference(stat_img, threshold=7, alpha=0.05)
```

### Step 5: Assign vals = get_data(...)

```python
vals = get_data(th_map)
```

**Verification:**
```python
assert np.sum(vals > 0) == 1
```


## Complete Example

```python
# Setup
# Fixtures: data_norm_isf, affine_eye

# Workflow
data = data_norm_isf
data[3, 6, 7] = 10
stat_img = Nifti1Image(data, affine_eye)
th_map = cluster_level_inference(stat_img, threshold=7, alpha=0.05)
vals = get_data(th_map)
assert np.sum(vals > 0) == 1
```

## Next Steps


---

*Source: test_thresholding.py:418 | Complexity: Intermediate | Last updated: 2026-05-18*