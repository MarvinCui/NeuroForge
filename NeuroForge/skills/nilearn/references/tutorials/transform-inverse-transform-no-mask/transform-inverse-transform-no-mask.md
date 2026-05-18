# How To: Transform Inverse Transform No Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check output of inverse transform when not using a mask.

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

### Step 1: 'Check output of inverse transform when not using a mask.'

```python
'Check output of inverse transform when not using a mask.'
```

**Verification:**
```python
assert np.array_equal(signals[0], [1, 2, 3, 4, 10, 20, 30, 40, 50])
```

### Step 2: Assign img_data = value

```python
img_data = {}
```

**Verification:**
```python
assert_polydata_equal(img.data, unmasked_img.data)
```

### Step 3: Assign img = SurfaceImage(...)

```python
img = SurfaceImage(surf_mesh, img_data)
```

### Step 4: Assign masker = SurfaceMasker.fit(...)

```python
masker = SurfaceMasker(standardize=None).fit(img)
```

### Step 5: Assign signals = masker.transform(...)

```python
signals = masker.transform(img)
```

**Verification:**
```python
assert np.array_equal(signals[0], [1, 2, 3, 4, 10, 20, 30, 40, 50])
```

### Step 6: Assign unmasked_img = masker.inverse_transform(...)

```python
unmasked_img = masker.inverse_transform(signals)
```

### Step 7: Call assert_polydata_equal()

```python
assert_polydata_equal(img.data, unmasked_img.data)
```

### Step 8: Assign data_shape = value

```python
data_shape = (val.n_vertices, n_timepoints)
```

### Step 9: Assign data_part = value

```python
data_part = (np.arange(np.prod(data_shape)).reshape(data_shape[::-1]) + 1.0) * 10 ** i
```

### Step 10: Assign unknown = value

```python
img_data[key] = data_part.T
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, n_timepoints

# Workflow
'Check output of inverse transform when not using a mask.'
img_data = {}
for i, (key, val) in enumerate(surf_mesh.parts.items()):
    data_shape = (val.n_vertices, n_timepoints)
    data_part = (np.arange(np.prod(data_shape)).reshape(data_shape[::-1]) + 1.0) * 10 ** i
    img_data[key] = data_part.T
img = SurfaceImage(surf_mesh, img_data)
masker = SurfaceMasker(standardize=None).fit(img)
signals = masker.transform(img)
assert np.array_equal(signals[0], [1, 2, 3, 4, 10, 20, 30, 40, 50])
unmasked_img = masker.inverse_transform(signals)
assert_polydata_equal(img.data, unmasked_img.data)
```

## Next Steps


---

*Source: test_surface_masker.py:61 | Complexity: Advanced | Last updated: 2026-05-18*