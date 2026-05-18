# How To: Transform Inverse Transform With Mask

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check output of inverse transform when using a mask.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.maskers`
- `nilearn.surface`
- `nilearn.surface.utils`

**Setup Required:**
```python
# Fixtures: surf_mesh, n_timepoints
```

## Step-by-Step Guide

### Step 1: 'Check output of inverse transform when using a mask.'

```python
'Check output of inverse transform when using a mask.'
```

**Verification:**
```python
assert np.array_equal(signals.ravel()[:7], [2, 3, 4, 20, 30, 40, 50])
```

### Step 2: Assign img_data = value

```python
img_data = {}
```

**Verification:**
```python
assert_surface_image_equal(unmasked_img, expected_img)
```

### Step 3: Assign img = SurfaceImage(...)

```python
img = SurfaceImage(surf_mesh, img_data)
```

### Step 4: Assign mask_data = value

```python
mask_data = {'left': np.asarray([False, True, True, True]), 'right': np.asarray([False, True, True, True, True])}
```

### Step 5: Assign mask = SurfaceImage(...)

```python
mask = SurfaceImage(surf_mesh, mask_data)
```

### Step 6: Assign masker = SurfaceMasker.fit(...)

```python
masker = SurfaceMasker(mask, standardize=None).fit(img)
```

### Step 7: Assign signals = masker.transform(...)

```python
signals = masker.transform(img)
```

**Verification:**
```python
assert np.array_equal(signals.ravel()[:7], [2, 3, 4, 20, 30, 40, 50])
```

### Step 8: Assign unmasked_img = masker.inverse_transform(...)

```python
unmasked_img = masker.inverse_transform(signals)
```

### Step 9: Assign expected_data = value

```python
expected_data = {k: v.copy() for k, v in img.data.parts.items()}
```

### Step 10: Assign expected_img = SurfaceImage(...)

```python
expected_img = SurfaceImage(img.mesh, expected_data)
```

### Step 11: Call assert_surface_image_equal()

```python
assert_surface_image_equal(unmasked_img, expected_img)
```

### Step 12: Assign data_shape = value

```python
data_shape = (val.n_vertices, n_timepoints)
```

### Step 13: Assign data_part = value

```python
data_part = (np.arange(np.prod(data_shape)).reshape(data_shape[::-1]) + 1.0) * 10 ** i
```

### Step 14: Assign unknown = value

```python
img_data[key] = data_part.T
```

### Step 15: Assign unknown = 0.0

```python
v[0] = 0.0
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, n_timepoints

# Workflow
'Check output of inverse transform when using a mask.'
img_data = {}
for i, (key, val) in enumerate(surf_mesh.parts.items()):
    data_shape = (val.n_vertices, n_timepoints)
    data_part = (np.arange(np.prod(data_shape)).reshape(data_shape[::-1]) + 1.0) * 10 ** i
    img_data[key] = data_part.T
img = SurfaceImage(surf_mesh, img_data)
mask_data = {'left': np.asarray([False, True, True, True]), 'right': np.asarray([False, True, True, True, True])}
mask = SurfaceImage(surf_mesh, mask_data)
masker = SurfaceMasker(mask, standardize=None).fit(img)
signals = masker.transform(img)
assert np.array_equal(signals.ravel()[:7], [2, 3, 4, 20, 30, 40, 50])
unmasked_img = masker.inverse_transform(signals)
expected_data = {k: v.copy() for k, v in img.data.parts.items()}
for v in expected_data.values():
    v[0] = 0.0
expected_img = SurfaceImage(img.mesh, expected_data)
assert_surface_image_equal(unmasked_img, expected_img)
```

## Next Steps


---

*Source: test_surface_masker.py:84 | Complexity: Advanced | Last updated: 2026-05-18*