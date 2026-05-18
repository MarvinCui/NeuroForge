# How To: Inverse Transform Actual Output

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that inverse_transform returns the expected output.

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

### Step 1: 'Test that inverse_transform returns the expected output.'

```python
'Test that inverse_transform returns the expected output.'
```

**Verification:**
```python
assert np.allclose(X_inverse_transformed.data.parts['left'], img_data['left'])
```

### Step 2: Assign A = rng.random(...)

```python
A = rng.random((9, 2))
```

**Verification:**
```python
assert np.allclose(X_inverse_transformed.data.parts['right'], img_data['right'])
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

### Step 9: Assign masker = SurfaceMapsMasker.fit(...)

```python
masker = SurfaceMapsMasker(surf_maps_img, standardize=None).fit()
```

### Step 10: Assign region_signals = masker.fit_transform(...)

```python
region_signals = masker.fit_transform(surf_img)
```

### Step 11: Assign X_inverse_transformed = masker.inverse_transform(...)

```python
X_inverse_transformed = masker.inverse_transform(region_signals)
```

**Verification:**
```python
assert np.allclose(X_inverse_transformed.data.parts['left'], img_data['left'])
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, rng

# Workflow
'Test that inverse_transform returns the expected output.'
A = rng.random((9, 2))
maps_data = {'left': A[:4, :], 'right': A[4:, :]}
surf_maps_img = SurfaceImage(surf_mesh, maps_data)
expected_region_signals = rng.random((50, 2))
B = np.dot(A, expected_region_signals.T)
img_data = {'left': B[:4, :], 'right': B[4:, :]}
surf_img = SurfaceImage(surf_mesh, img_data)
masker = SurfaceMapsMasker(surf_maps_img, standardize=None).fit()
region_signals = masker.fit_transform(surf_img)
X_inverse_transformed = masker.inverse_transform(region_signals)
assert np.allclose(X_inverse_transformed.data.parts['left'], img_data['left'])
assert np.allclose(X_inverse_transformed.data.parts['right'], img_data['right'])
```

## Next Steps


---

*Source: test_surface_maps_masker.py:101 | Complexity: Advanced | Last updated: 2026-05-18*