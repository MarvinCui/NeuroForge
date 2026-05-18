# How To: Real Sh Tournier

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test real sh tournier

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.interpolation`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign vertices = value

```python
vertices = hemi_icosahedron.subdivide(n=2).vertices
```

**Verification:**
```python
assert_array_almost_equal(sf_approx, sf, 2)
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array([[0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]])
```

### Step 3: Assign angles = value

```python
angles = [(0, 0), (60, 0)]
```

### Step 4: Assign odf = multi_tensor_odf(...)

```python
odf = multi_tensor_odf(vertices, mevals, angles, [50, 50])
```

### Step 5: Assign mevals = np.array(...)

```python
mevals = np.array([[0.0015, 0.0003, 0.0003]])
```

### Step 6: Assign angles = value

```python
angles = [(0, 0)]
```

### Step 7: Assign odf2 = multi_tensor_odf(...)

```python
odf2 = multi_tensor_odf(-vertices, mevals, angles, [100])
```

### Step 8: Assign sphere = Sphere(...)

```python
sphere = Sphere(xyz=np.vstack((vertices, -vertices)))
```

### Step 9: Assign sf = np.append(...)

```python
sf = np.append(odf, odf2)
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(len(w), 1)
```

### Step 11: Call npt.assert_()

```python
npt.assert_(issubclass(w[0].category, PendingDeprecationWarning))
```

### Step 12: Call npt.assert_()

```python
npt.assert_(tournier07_legacy_msg in str(w[0].message))
```

### Step 13: Assign invB = smooth_pinv(...)

```python
invB = smooth_pinv(B, L=np.zeros_like(l_values))
```

### Step 14: Assign sh_coefs = np.dot(...)

```python
sh_coefs = np.dot(invB, sf)
```

### Step 15: Assign sf_approx = np.dot(...)

```python
sf_approx = np.dot(B, sh_coefs)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sf_approx, sf, 2)
```

### Step 17: Assign unknown = real_sh_tournier(...)

```python
B, m_values, l_values = real_sh_tournier(10, sphere.theta, sphere.phi, full_basis=True)
```


## Complete Example

```python
# Workflow
vertices = hemi_icosahedron.subdivide(n=2).vertices
mevals = np.array([[0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]])
angles = [(0, 0), (60, 0)]
odf = multi_tensor_odf(vertices, mevals, angles, [50, 50])
mevals = np.array([[0.0015, 0.0003, 0.0003]])
angles = [(0, 0)]
odf2 = multi_tensor_odf(-vertices, mevals, angles, [100])
sphere = Sphere(xyz=np.vstack((vertices, -vertices)))
sf = np.append(odf, odf2)
with warnings.catch_warnings(record=True) as w:
    B, m_values, l_values = real_sh_tournier(10, sphere.theta, sphere.phi, full_basis=True)
npt.assert_equal(len(w), 1)
npt.assert_(issubclass(w[0].category, PendingDeprecationWarning))
npt.assert_(tournier07_legacy_msg in str(w[0].message))
invB = smooth_pinv(B, L=np.zeros_like(l_values))
sh_coefs = np.dot(invB, sf)
sf_approx = np.dot(B, sh_coefs)
assert_array_almost_equal(sf_approx, sf, 2)
```

## Next Steps


---

*Source: test_shm.py:284 | Complexity: Advanced | Last updated: 2026-05-18*