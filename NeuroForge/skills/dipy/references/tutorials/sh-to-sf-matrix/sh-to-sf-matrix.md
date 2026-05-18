# How To: Sh To Sf Matrix

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sh to sf matrix

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

### Step 1: Assign sphere = Sphere(...)

```python
sphere = Sphere(xyz=hemi_icosahedron.vertices)
```

**Verification:**
```python
assert_array_almost_equal(B1, B2.T)
```

### Step 2: Assign invB2 = smooth_pinv(...)

```python
invB2 = smooth_pinv(B2, L=np.zeros_like(l_values))
```

**Verification:**
```python
assert_array_almost_equal(invB1, invB2.T)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(B1, B2.T)
```

**Verification:**
```python
assert_array_almost_equal(B3, B1)
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(invB1, invB2.T)
```

**Verification:**
```python
assert_raises(ValueError, sh_to_sf_matrix, sphere, basis_type='')
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(B3, B1)
```

### Step 6: Call assert_raises()

```python
assert_raises(ValueError, sh_to_sf_matrix, sphere, basis_type='')
```

### Step 7: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 8: Assign unknown = sh_to_sf_matrix(...)

```python
B1, invB1 = sh_to_sf_matrix(sphere)
```

### Step 9: Assign unknown = real_sh_descoteaux(...)

```python
B2, m_values, l_values = real_sh_descoteaux(4, sphere.theta, sphere.phi)
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 11: Assign B3 = sh_to_sf_matrix(...)

```python
B3 = sh_to_sf_matrix(sphere, return_inv=False)
```


## Complete Example

```python
# Workflow
sphere = Sphere(xyz=hemi_icosahedron.vertices)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    B1, invB1 = sh_to_sf_matrix(sphere)
    B2, m_values, l_values = real_sh_descoteaux(4, sphere.theta, sphere.phi)
invB2 = smooth_pinv(B2, L=np.zeros_like(l_values))
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    B3 = sh_to_sf_matrix(sphere, return_inv=False)
assert_array_almost_equal(B1, B2.T)
assert_array_almost_equal(invB1, invB2.T)
assert_array_almost_equal(B3, B1)
assert_raises(ValueError, sh_to_sf_matrix, sphere, basis_type='')
```

## Next Steps


---

*Source: test_shm.py:350 | Complexity: Advanced | Last updated: 2026-05-18*