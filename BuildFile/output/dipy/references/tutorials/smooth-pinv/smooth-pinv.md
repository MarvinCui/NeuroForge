# How To: Smooth Pinv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test smooth pinv

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

### Step 1: Assign hemi = hemi_icosahedron.subdivide(...)

```python
hemi = hemi_icosahedron.subdivide(n=2)
```

**Verification:**
```python
assert_array_almost_equal(C, D)
```

### Step 2: Assign unknown = sph_harm_ind_list(...)

```python
m_values, l_values = sph_harm_ind_list(4)
```

**Verification:**
```python
assert_array_almost_equal(C, D)
```

### Step 3: Assign L = np.zeros(...)

```python
L = np.zeros(len(m_values))
```

**Verification:**
```python
assert_array_almost_equal(C, D)
```

### Step 4: Assign C = smooth_pinv(...)

```python
C = smooth_pinv(B, L)
```

### Step 5: Assign D = np.dot(...)

```python
D = np.dot(npl.inv(np.dot(B.T, B)), B.T)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(C, D)
```

### Step 7: Assign L = value

```python
L = l_values * (l_values + 1) * 0.05
```

### Step 8: Assign C = smooth_pinv(...)

```python
C = smooth_pinv(B, L)
```

### Step 9: Assign L = np.diag(...)

```python
L = np.diag(L)
```

### Step 10: Assign D = np.dot(...)

```python
D = np.dot(npl.inv(np.dot(B.T, B) + L * L), B.T)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(C, D)
```

### Step 12: Assign L = value

```python
L = np.arange(len(l_values)) * 0.05
```

### Step 13: Assign C = smooth_pinv(...)

```python
C = smooth_pinv(B, L)
```

### Step 14: Assign L = np.diag(...)

```python
L = np.diag(L)
```

### Step 15: Assign D = np.dot(...)

```python
D = np.dot(npl.inv(np.dot(B.T, B) + L * L), B.T)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(C, D)
```

### Step 17: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 18: Assign B = real_sh_descoteaux_from_index(...)

```python
B = real_sh_descoteaux_from_index(m_values, l_values, hemi.theta[:, None], hemi.phi[:, None])
```


## Complete Example

```python
# Workflow
hemi = hemi_icosahedron.subdivide(n=2)
m_values, l_values = sph_harm_ind_list(4)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    B = real_sh_descoteaux_from_index(m_values, l_values, hemi.theta[:, None], hemi.phi[:, None])
L = np.zeros(len(m_values))
C = smooth_pinv(B, L)
D = np.dot(npl.inv(np.dot(B.T, B)), B.T)
assert_array_almost_equal(C, D)
L = l_values * (l_values + 1) * 0.05
C = smooth_pinv(B, L)
L = np.diag(L)
D = np.dot(npl.inv(np.dot(B.T, B) + L * L), B.T)
assert_array_almost_equal(C, D)
L = np.arange(len(l_values)) * 0.05
C = smooth_pinv(B, L)
L = np.diag(L)
D = np.dot(npl.inv(np.dot(B.T, B) + L * L), B.T)
assert_array_almost_equal(C, D)
```

## Next Steps


---

*Source: test_shm.py:381 | Complexity: Advanced | Last updated: 2026-05-18*