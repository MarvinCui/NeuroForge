# How To: Real Sym Sh Basis

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test real sym sh basis

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

### Step 1: Assign new_order = value

```python
new_order = [0, 5, 4, 3, 2, 1, 14, 13, 12, 11, 10, 9, 8, 7, 6]
```

**Verification:**
```python
assert_array_almost_equal(descoteaux07_basis, expected)
```

### Step 2: Assign sphere = hemi_icosahedron.subdivide(...)

```python
sphere = hemi_icosahedron.subdivide(n=2)
```

### Step 3: Assign expected = value

```python
expected = basis[:, new_order]
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(len(w), 2)
```

### Step 5: Call npt.assert_()

```python
npt.assert_(issubclass(w[0].category, DeprecationWarning))
```

### Step 6: Call npt.assert_()

```python
npt.assert_('dipy.reconst.shm.real_sym_sh_basis is deprecated, Please use dipy.reconst.shm.real_sh_descoteaux instead' in str(w[0].message))
```

### Step 7: Call npt.assert_()

```python
npt.assert_(issubclass(w[1].category, PendingDeprecationWarning))
```

### Step 8: Call npt.assert_()

```python
npt.assert_(descoteaux07_legacy_msg in str(w[1].message))
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(descoteaux07_basis, expected)
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore')
```

### Step 11: Assign unknown = real_sym_sh_mrtrix(...)

```python
basis, m_values, l_values = real_sym_sh_mrtrix(4, sphere.theta, sphere.phi)
```

### Step 12: Assign unknown = real_sym_sh_basis(...)

```python
descoteaux07_basis, m_values, l_values = real_sym_sh_basis(4, sphere.theta, sphere.phi)
```


## Complete Example

```python
# Workflow
new_order = [0, 5, 4, 3, 2, 1, 14, 13, 12, 11, 10, 9, 8, 7, 6]
sphere = hemi_icosahedron.subdivide(n=2)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore')
    basis, m_values, l_values = real_sym_sh_mrtrix(4, sphere.theta, sphere.phi)
expected = basis[:, new_order]
expected *= np.where(m_values == 0, 1.0, np.sqrt(2))
with warnings.catch_warnings(record=True) as w:
    descoteaux07_basis, m_values, l_values = real_sym_sh_basis(4, sphere.theta, sphere.phi)
npt.assert_equal(len(w), 2)
npt.assert_(issubclass(w[0].category, DeprecationWarning))
npt.assert_('dipy.reconst.shm.real_sym_sh_basis is deprecated, Please use dipy.reconst.shm.real_sh_descoteaux instead' in str(w[0].message))
npt.assert_(issubclass(w[1].category, PendingDeprecationWarning))
npt.assert_(descoteaux07_legacy_msg in str(w[1].message))
assert_array_almost_equal(descoteaux07_basis, expected)
```

## Next Steps


---

*Source: test_shm.py:229 | Complexity: Advanced | Last updated: 2026-05-18*