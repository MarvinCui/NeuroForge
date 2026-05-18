# How To: Fit Transform Actual Output

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that fit_transform returns the expected output.
Meaning that the SurfaceMapsMasker gives the solution to equation Ax = B,
where A is the maps_img, x is the region_signals, and B is the img.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.maskers`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: surf_mesh, rng
```

## Step-by-Step Guide

### Step 1: 'Test that fit_transform returns the expected output.\n    Meaning that the SurfaceMapsMasker gives the solution to equation Ax = B,\n    where A is the maps_img, x is the region_signals, and B is the img.\n    '

```python
'Test that fit_transform returns the expected output.\n    Meaning that the SurfaceMapsMasker gives the solution to equation Ax = B,\n    where A is the maps_img, x is the region_signals, and B is the img.\n    '
```

**Verification:**
```python
assert region_signals.shape == expected_region_signals.shape
```

### Step 2: Assign A = rng.random(...)

```python
A = rng.random((9, 2))
```

**Verification:**
```python
assert np.allclose(region_signals, expected_region_signals)
```

### Step 3: Assign maps_data = value

```python
maps_data = {'left': A[:4, :], 'right': A[4:, :]}
```

### Step 4: Assign surf_maps_img = SurfaceImage(...)

```python
surf_maps_img = SurfaceImage(surf_mesh, maps_data)
```

### Step 5: Assign expected_region_signals = rng.random(...)

```python
expected_region_signals = rng.random((50, 2))
```

### Step 6: Assign B = np.dot(...)

```python
B = np.dot(A, expected_region_signals.T)
```

### Step 7: Assign img_data = value

```python
img_data = {'left': B[:4, :], 'right': B[4:, :]}
```

### Step 8: Assign surf_img = SurfaceImage(...)

```python
surf_img = SurfaceImage(surf_mesh, img_data)
```

### Step 9: Assign region_signals = SurfaceMapsMasker.fit_transform(...)

```python
region_signals = SurfaceMapsMasker(surf_maps_img, standardize=None).fit_transform(surf_img)
```

**Verification:**
```python
assert region_signals.shape == expected_region_signals.shape
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, rng

# Workflow
'Test that fit_transform returns the expected output.\n    Meaning that the SurfaceMapsMasker gives the solution to equation Ax = B,\n    where A is the maps_img, x is the region_signals, and B is the img.\n    '
A = rng.random((9, 2))
maps_data = {'left': A[:4, :], 'right': A[4:, :]}
surf_maps_img = SurfaceImage(surf_mesh, maps_data)
expected_region_signals = rng.random((50, 2))
B = np.dot(A, expected_region_signals.T)
img_data = {'left': B[:4, :], 'right': B[4:, :]}
surf_img = SurfaceImage(surf_mesh, img_data)
region_signals = SurfaceMapsMasker(surf_maps_img, standardize=None).fit_transform(surf_img)
assert region_signals.shape == expected_region_signals.shape
assert np.allclose(region_signals, expected_region_signals)
```

## Next Steps


---

*Source: test_surface_maps_masker.py:74 | Complexity: Advanced | Last updated: 2026-05-18*