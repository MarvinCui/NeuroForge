# How To: Invert Vector Field 3D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Inverts a synthetic, analytically invertible, displacement field

## Prerequisites

**Required Modules:**
- `nibabel.affines`
- `numpy`
- `numpy.testing`
- `scipy.ndimage`
- `dipy.align`
- `dipy.align.parzenhist`
- `dipy.align.transforms`
- `dipy.core`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: '\n    Inverts a synthetic, analytically invertible, displacement field\n    '

```python
'\n    Inverts a synthetic, analytically invertible, displacement field\n    '
```

**Verification:**
```python
assert_almost_equal(stats[1], 0, decimal=3)
```

### Step 2: Assign shape = value

```python
shape = (64, 64, 64)
```

**Verification:**
```python
assert_almost_equal(stats[2], 0, decimal=3)
```

### Step 3: Assign ns = value

```python
ns = shape[0]
```

**Verification:**
```python
assert_raises(ValueError, vfu.invert_vector_field_fixed_point_3d, d, invalid, spacing, 40, 1e-07, start=None)
```

### Step 4: Assign nr = value

```python
nr = shape[1]
```

### Step 5: Assign nc = value

```python
nc = shape[2]
```

### Step 6: Assign axis = np.array(...)

```python
axis = np.array([2.0, 0.5, 1.0])
```

### Step 7: Assign t = 2.5

```python
t = 2.5
```

### Step 8: Assign trans = np.array(...)

```python
trans = np.array([[1, 0, 0, -t * ns], [0, 1, 0, -t * nr], [0, 0, 1, -t * nc], [0, 0, 0, 1]])
```

### Step 9: Assign trans_inv = np.linalg.inv(...)

```python
trans_inv = np.linalg.inv(trans)
```

### Step 10: Assign unknown = vfu.create_harmonic_fields_3d(...)

```python
d, _ = vfu.create_harmonic_fields_3d(ns, nr, nc, 0.2, 8)
```

### Step 11: Assign d = np.asarray.astype(...)

```python
d = np.asarray(d).astype(floating)
```

### Step 12: Assign invalid = np.zeros(...)

```python
invalid = np.zeros((3, 3), dtype=np.float64)
```

### Step 13: Assign spacing = np.array(...)

```python
spacing = np.array([1.0, 1.0, 1.0])
```

### Step 14: Call assert_raises()

```python
assert_raises(ValueError, vfu.invert_vector_field_fixed_point_3d, d, invalid, spacing, 40, 1e-07, start=None)
```

### Step 15: Assign rot = np.zeros(...)

```python
rot = np.zeros(shape=(4, 4))
```

### Step 16: Assign unknown = geometry.rodrigues_axis_rotation(...)

```python
rot[:3, :3] = geometry.rodrigues_axis_rotation(axis, theta)
```

### Step 17: Assign unknown = 1.0

```python
rot[3, 3] = 1.0
```

### Step 18: Assign scale = np.array(...)

```python
scale = np.array([[1 * s, 0, 0, 0], [0, 1 * s, 0, 0], [0, 0, 1 * s, 0], [0, 0, 0, 1]])
```

### Step 19: Assign gt_affine = trans_inv.dot(...)

```python
gt_affine = trans_inv.dot(scale.dot(rot.dot(trans)))
```

### Step 20: Assign gt_affine_inv = np.linalg.inv(...)

```python
gt_affine_inv = np.linalg.inv(gt_affine)
```

### Step 21: Assign dcopy = np.copy(...)

```python
dcopy = np.copy(d)
```

### Step 22: Call vfu.reorient_vector_field_3d()

```python
vfu.reorient_vector_field_3d(dcopy, gt_affine)
```

### Step 23: Assign inv_approx = vfu.invert_vector_field_fixed_point_3d(...)

```python
inv_approx = vfu.invert_vector_field_fixed_point_3d(dcopy, gt_affine_inv, np.array([s, s, s]) * 0.5, 40, 1e-07)
```

### Step 24: Assign mapping = imwarp.DiffeomorphicMap(...)

```python
mapping = imwarp.DiffeomorphicMap(3, (nr, nc), disp_grid2world=gt_affine)
```

### Step 25: Assign mapping.forward = dcopy

```python
mapping.forward = dcopy
```

### Step 26: Assign mapping.backward = inv_approx

```python
mapping.backward = inv_approx
```

### Step 27: Assign unknown = mapping.compute_inversion_error(...)

```python
residual, stats = mapping.compute_inversion_error()
```

### Step 28: Call assert_almost_equal()

```python
assert_almost_equal(stats[1], 0, decimal=3)
```

### Step 29: Call assert_almost_equal()

```python
assert_almost_equal(stats[2], 0, decimal=3)
```


## Complete Example

```python
# Workflow
'\n    Inverts a synthetic, analytically invertible, displacement field\n    '
shape = (64, 64, 64)
ns = shape[0]
nr = shape[1]
nc = shape[2]
axis = np.array([2.0, 0.5, 1.0])
t = 2.5
trans = np.array([[1, 0, 0, -t * ns], [0, 1, 0, -t * nr], [0, 0, 1, -t * nc], [0, 0, 0, 1]])
trans_inv = np.linalg.inv(trans)
d, _ = vfu.create_harmonic_fields_3d(ns, nr, nc, 0.2, 8)
d = np.asarray(d).astype(floating)
for theta in [-1 * np.pi / 5.0, 0.0, np.pi / 5.0]:
    for s in [0.5, 1.0, 2.0]:
        rot = np.zeros(shape=(4, 4))
        rot[:3, :3] = geometry.rodrigues_axis_rotation(axis, theta)
        rot[3, 3] = 1.0
        scale = np.array([[1 * s, 0, 0, 0], [0, 1 * s, 0, 0], [0, 0, 1 * s, 0], [0, 0, 0, 1]])
        gt_affine = trans_inv.dot(scale.dot(rot.dot(trans)))
        gt_affine_inv = np.linalg.inv(gt_affine)
        dcopy = np.copy(d)
        vfu.reorient_vector_field_3d(dcopy, gt_affine)
        inv_approx = vfu.invert_vector_field_fixed_point_3d(dcopy, gt_affine_inv, np.array([s, s, s]) * 0.5, 40, 1e-07)
        mapping = imwarp.DiffeomorphicMap(3, (nr, nc), disp_grid2world=gt_affine)
        mapping.forward = dcopy
        mapping.backward = inv_approx
        residual, stats = mapping.compute_inversion_error()
        assert_almost_equal(stats[1], 0, decimal=3)
        assert_almost_equal(stats[2], 0, decimal=3)
invalid = np.zeros((3, 3), dtype=np.float64)
spacing = np.array([1.0, 1.0, 1.0])
assert_raises(ValueError, vfu.invert_vector_field_fixed_point_3d, d, invalid, spacing, 40, 1e-07, start=None)
```

## Next Steps


---

*Source: test_vector_fields.py:1230 | Complexity: Advanced | Last updated: 2026-05-18*