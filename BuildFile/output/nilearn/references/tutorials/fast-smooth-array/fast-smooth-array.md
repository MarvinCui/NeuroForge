# How To: Fast Smooth Array

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fast smooth array

## Prerequisites

**Required Modules:**
- `platform`
- `re`
- `warnings`
- `collections.abc`
- `pathlib`
- `joblib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `nibabel.freesurfer`
- `numpy.testing`
- `nilearn`
- `nilearn`
- `nilearn._utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.niimg`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image.image`
- `nilearn.image.resampling`
- `nilearn.image.tests._testing`
- `nilearn.surface.surface`
- `nilearn.surface.surface`
- `nilearn.surface.utils`


## Step-by-Step Guide

### Step 1: Assign N = 4

```python
N = 4
```

**Verification:**
```python
assert_allclose(smooth_data, expected)
```

### Step 2: Assign shape = value

```python
shape = (N, N, N)
```

### Step 3: Assign neighbor_weight = 0.2

```python
neighbor_weight = 0.2
```

### Step 4: Assign n_neighbors_max = 6

```python
n_neighbors_max = 6
```

### Step 5: Assign data = np.ones(...)

```python
data = np.ones(shape)
```

### Step 6: Assign smooth_data = _fast_smooth_array(...)

```python
smooth_data = _fast_smooth_array(data)
```

### Step 7: Assign n_neighbors_arr = np.empty(...)

```python
n_neighbors_arr = np.empty(shape)
```

### Step 8: Assign expected = value

```python
expected = (1 + neighbor_weight * n_neighbors_arr) / (1 + neighbor_weight * n_neighbors_max)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(smooth_data, expected)
```

### Step 10: Assign unknown = value

```python
n_neighbors_arr[i, j, k] = 3 + (0 < i < N - 1) + (0 < j < N - 1) + (0 < k < N - 1)
```


## Complete Example

```python
# Workflow
N = 4
shape = (N, N, N)
neighbor_weight = 0.2
n_neighbors_max = 6
data = np.ones(shape)
smooth_data = _fast_smooth_array(data)
n_neighbors_arr = np.empty(shape)
for (i, j, k), __ in np.ndenumerate(n_neighbors_arr):
    n_neighbors_arr[i, j, k] = 3 + (0 < i < N - 1) + (0 < j < N - 1) + (0 < k < N - 1)
expected = (1 + neighbor_weight * n_neighbors_arr) / (1 + neighbor_weight * n_neighbors_max)
assert_allclose(smooth_data, expected)
```

## Next Steps


---

*Source: test_image.py:259 | Complexity: Advanced | Last updated: 2026-05-18*