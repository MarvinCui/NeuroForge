# How To: Diffeomorphic Map Simplification 2D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test simplification of 2D diffeomorphic maps

Create an invertible deformation field, and define a DiffeomorphicMap
using different voxel-to-space transforms for domain, codomain, and
reference discretizations, also use a non-identity pre-aligning matrix.
Warp a circle using the diffeomorphic map to obtain the expected warped
circle. Now simplify the DiffeomorphicMap and warp the same circle
using this simplified map. Verify that the two warped circles are equal
up to numerical precision.

## Prerequisites

**Required Modules:**
- `nibabel.eulerangles`
- `numpy`
- `numpy.testing`
- `dipy.align`
- `dipy.align.imwarp`
- `dipy.core.interpolation`
- `dipy.data`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: 'Test simplification of 2D diffeomorphic maps\n\n    Create an invertible deformation field, and define a DiffeomorphicMap\n    using different voxel-to-space transforms for domain, codomain, and\n    reference discretizations, also use a non-identity pre-aligning matrix.\n    Warp a circle using the diffeomorphic map to obtain the expected warped\n    circle. Now simplify the DiffeomorphicMap and warp the same circle\n    using this simplified map. Verify that the two warped circles are equal\n    up to numerical precision.\n    '

```python
'Test simplification of 2D diffeomorphic maps\n\n    Create an invertible deformation field, and define a DiffeomorphicMap\n    using different voxel-to-space transforms for domain, codomain, and\n    reference discretizations, also use a non-identity pre-aligning matrix.\n    Warp a circle using the diffeomorphic map to obtain the expected warped\n    circle. Now simplify the DiffeomorphicMap and warp the same circle\n    using this simplified map. Verify that the two warped circles are equal\n    up to numerical precision.\n    '
```

**Verification:**
```python
assert_array_almost_equal(warped, expected)
```

### Step 2: Assign dom_shape = value

```python
dom_shape = (64, 64)
```

**Verification:**
```python
assert_equal(simplified.domain_grid2world, None)
```

### Step 3: Assign cod_shape = value

```python
cod_shape = (80, 80)
```

**Verification:**
```python
assert_equal(simplified.codomain_grid2world, None)
```

### Step 4: Assign nr = value

```python
nr = dom_shape[0]
```

**Verification:**
```python
assert_equal(simplified.disp_grid2world, None)
```

### Step 5: Assign nc = value

```python
nc = dom_shape[1]
```

**Verification:**
```python
assert_equal(simplified.domain_world2grid, None)
```

### Step 6: Assign s = 1.1

```python
s = 1.1
```

**Verification:**
```python
assert_equal(simplified.codomain_world2grid, None)
```

### Step 7: Assign t = 0.25

```python
t = 0.25
```

**Verification:**
```python
assert_equal(simplified.disp_world2grid, None)
```

### Step 8: Assign trans = np.array(...)

```python
trans = np.array([[1, 0, -t * nr], [0, 1, -t * nc], [0, 0, 1]])
```

### Step 9: Assign trans_inv = np.linalg.inv(...)

```python
trans_inv = np.linalg.inv(trans)
```

### Step 10: Assign scale = np.array(...)

```python
scale = np.array([[1 * s, 0, 0], [0, 1 * s, 0], [0, 0, 1]])
```

### Step 11: Assign gt_affine = trans_inv.dot(...)

```python
gt_affine = trans_inv.dot(scale.dot(trans))
```

### Step 12: Assign radius = 16

```python
radius = 16
```

### Step 13: Assign circle = vfu.create_circle(...)

```python
circle = vfu.create_circle(cod_shape[0], cod_shape[1], radius)
```

### Step 14: Assign unknown = vfu.create_harmonic_fields_2d(...)

```python
d, dinv = vfu.create_harmonic_fields_2d(dom_shape[0], dom_shape[1], 0.3, 6)
```

### Step 15: Assign D = gt_affine

```python
D = gt_affine
```

### Step 16: Assign C = imwarp.mult_aff(...)

```python
C = imwarp.mult_aff(gt_affine, gt_affine)
```

### Step 17: Assign R = np.eye(...)

```python
R = np.eye(3)
```

### Step 18: Assign P = gt_affine

```python
P = gt_affine
```

### Step 19: Assign diff_map = imwarp.DiffeomorphicMap(...)

```python
diff_map = imwarp.DiffeomorphicMap(dim=2, disp_shape=dom_shape, disp_grid2world=R, domain_shape=dom_shape, domain_grid2world=D, codomain_shape=cod_shape, codomain_grid2world=C, prealign=P)
```

### Step 20: Assign diff_map.forward = np.array(...)

```python
diff_map.forward = np.array(d, dtype=floating)
```

### Step 21: Assign diff_map.backward = np.array(...)

```python
diff_map.backward = np.array(dinv, dtype=floating)
```

### Step 22: Assign expected = diff_map.transform(...)

```python
expected = diff_map.transform(circle, interpolation='linear')
```

### Step 23: Assign simplified = diff_map.get_simplified_transform(...)

```python
simplified = diff_map.get_simplified_transform()
```

### Step 24: Assign warped = simplified.transform(...)

```python
warped = simplified.transform(circle, interpolation='linear')
```

### Step 25: Call assert_array_almost_equal()

```python
assert_array_almost_equal(warped, expected)
```

### Step 26: Call assert_equal()

```python
assert_equal(simplified.domain_grid2world, None)
```

### Step 27: Call assert_equal()

```python
assert_equal(simplified.codomain_grid2world, None)
```

### Step 28: Call assert_equal()

```python
assert_equal(simplified.disp_grid2world, None)
```

### Step 29: Call assert_equal()

```python
assert_equal(simplified.domain_world2grid, None)
```

### Step 30: Call assert_equal()

```python
assert_equal(simplified.codomain_world2grid, None)
```

### Step 31: Call assert_equal()

```python
assert_equal(simplified.disp_world2grid, None)
```


## Complete Example

```python
# Workflow
'Test simplification of 2D diffeomorphic maps\n\n    Create an invertible deformation field, and define a DiffeomorphicMap\n    using different voxel-to-space transforms for domain, codomain, and\n    reference discretizations, also use a non-identity pre-aligning matrix.\n    Warp a circle using the diffeomorphic map to obtain the expected warped\n    circle. Now simplify the DiffeomorphicMap and warp the same circle\n    using this simplified map. Verify that the two warped circles are equal\n    up to numerical precision.\n    '
dom_shape = (64, 64)
cod_shape = (80, 80)
nr = dom_shape[0]
nc = dom_shape[1]
s = 1.1
t = 0.25
trans = np.array([[1, 0, -t * nr], [0, 1, -t * nc], [0, 0, 1]])
trans_inv = np.linalg.inv(trans)
scale = np.array([[1 * s, 0, 0], [0, 1 * s, 0], [0, 0, 1]])
gt_affine = trans_inv.dot(scale.dot(trans))
radius = 16
circle = vfu.create_circle(cod_shape[0], cod_shape[1], radius)
d, dinv = vfu.create_harmonic_fields_2d(dom_shape[0], dom_shape[1], 0.3, 6)
D = gt_affine
C = imwarp.mult_aff(gt_affine, gt_affine)
R = np.eye(3)
P = gt_affine
diff_map = imwarp.DiffeomorphicMap(dim=2, disp_shape=dom_shape, disp_grid2world=R, domain_shape=dom_shape, domain_grid2world=D, codomain_shape=cod_shape, codomain_grid2world=C, prealign=P)
diff_map.forward = np.array(d, dtype=floating)
diff_map.backward = np.array(dinv, dtype=floating)
expected = diff_map.transform(circle, interpolation='linear')
simplified = diff_map.get_simplified_transform()
warped = simplified.transform(circle, interpolation='linear')
assert_array_almost_equal(warped, expected)
assert_equal(simplified.domain_grid2world, None)
assert_equal(simplified.codomain_grid2world, None)
assert_equal(simplified.disp_grid2world, None)
assert_equal(simplified.domain_world2grid, None)
assert_equal(simplified.codomain_world2grid, None)
assert_equal(simplified.disp_world2grid, None)
```

## Next Steps


---

*Source: test_imwarp.py:209 | Complexity: Advanced | Last updated: 2026-05-18*