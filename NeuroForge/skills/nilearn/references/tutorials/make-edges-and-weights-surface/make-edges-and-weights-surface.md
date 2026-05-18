# How To: Make Edges And Weights Surface

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Smoke test for _make_edges_and_weights_surface. Here we create a new
surface mask (relative to the one used in test_make_edges_surface) to make
sure overall edge and weight computation is robust.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `joblib`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.regions.rena_clustering`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: surf_mesh, surf_img_2d
```

## Step-by-Step Guide

### Step 1: 'Smoke test for _make_edges_and_weights_surface. Here we create a new\n    surface mask (relative to the one used in test_make_edges_surface) to make\n    sure overall edge and weight computation is robust.\n    '

```python
'Smoke test for _make_edges_and_weights_surface. Here we create a new\n    surface mask (relative to the one used in test_make_edges_surface) to make\n    sure overall edge and weight computation is robust.\n    '
```

**Verification:**
```python
assert len(edges) == 2
```

### Step 2: Assign data = value

```python
data = {'left': np.array([False, True, True, True]), 'right': np.array([True, True, False, True, False])}
```

**Verification:**
```python
assert len(weights) == 2
```

### Step 3: Assign surf_mask_1d = SurfaceImage(...)

```python
surf_mask_1d = SurfaceImage(surf_mesh, data)
```

**Verification:**
```python
assert part in edges
```

### Step 4: Assign masker = SurfaceMasker.fit(...)

```python
masker = SurfaceMasker(surf_mask_1d, standardize=None).fit()
```

**Verification:**
```python
assert part in weights
```

### Step 5: Assign X = masker.transform(...)

```python
X = masker.transform(surf_img_2d(50))
```

**Verification:**
```python
assert np.intersect1d(edges['left'], edges['right']).size == 0
```

### Step 6: Assign unknown = _make_edges_and_weights_surface(...)

```python
edges, weights = _make_edges_and_weights_surface(X, surf_mask_1d)
```

**Verification:**
```python
assert_array_equal(edges['left'], np.array([[0, 1, 0], [1, 2, 2]]))
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(edges['left'], np.array([[0, 1, 0], [1, 2, 2]]))
```

**Verification:**
```python
assert_array_equal(edges['right'], np.array([[3, 3, 4], [4, 5, 5]]))
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(edges['right'], np.array([[3, 3, 4], [4, 5, 5]]))
```

**Verification:**
```python
assert len(weights['left']) == 3
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, surf_img_2d

# Workflow
'Smoke test for _make_edges_and_weights_surface. Here we create a new\n    surface mask (relative to the one used in test_make_edges_surface) to make\n    sure overall edge and weight computation is robust.\n    '
data = {'left': np.array([False, True, True, True]), 'right': np.array([True, True, False, True, False])}
surf_mask_1d = SurfaceImage(surf_mesh, data)
masker = SurfaceMasker(surf_mask_1d, standardize=None).fit()
X = masker.transform(surf_img_2d(50))
edges, weights = _make_edges_and_weights_surface(X, surf_mask_1d)
assert len(edges) == 2
assert len(weights) == 2
for part in ['left', 'right']:
    assert part in edges
    assert part in weights
assert np.intersect1d(edges['left'], edges['right']).size == 0
assert_array_equal(edges['left'], np.array([[0, 1, 0], [1, 2, 2]]))
assert_array_equal(edges['right'], np.array([[3, 3, 4], [4, 5, 5]]))
assert len(weights['left']) == 3
assert len(weights['right']) == 3
```

## Next Steps


---

*Source: test_rena_clustering.py:150 | Complexity: Advanced | Last updated: 2026-05-18*