# How To: Hat And Lcr

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test hat and lcr

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
hemi = hemi_icosahedron.subdivide(n=3)
```

**Verification:**
```python
assert_array_almost_equal(B, B_hat)
```

### Step 2: Assign unknown = sph_harm_ind_list(...)

```python
m_values, l_values = sph_harm_ind_list(8)
```

**Verification:**
```python
assert_array_almost_equal(r, r2)
```

### Step 3: Assign H = hat(...)

```python
H = hat(B)
```

**Verification:**
```python
assert_array_almost_equal(r, r3)
```

### Step 4: Assign B_hat = np.dot(...)

```python
B_hat = np.dot(H, B)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(B, B_hat)
```

### Step 6: Assign R = lcr_matrix(...)

```python
R = lcr_matrix(H)
```

### Step 7: Assign d = np.arange(...)

```python
d = np.arange(len(hemi.theta))
```

### Step 8: Assign r = value

```python
r = d - np.dot(H, d)
```

### Step 9: Assign lev = np.sqrt(...)

```python
lev = np.sqrt(1 - H.diagonal())
```

### Step 10: Assign r2 = np.dot(...)

```python
r2 = np.dot(R, d)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(r, r2)
```

### Step 12: Assign r3 = np.dot(...)

```python
r3 = np.dot(d, R.T)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(r, r3)
```

### Step 14: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 15: Assign B = real_sh_descoteaux_from_index(...)

```python
B = real_sh_descoteaux_from_index(m_values, l_values, hemi.theta[:, None], hemi.phi[:, None])
```


## Complete Example

```python
# Workflow
hemi = hemi_icosahedron.subdivide(n=3)
m_values, l_values = sph_harm_ind_list(8)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    B = real_sh_descoteaux_from_index(m_values, l_values, hemi.theta[:, None], hemi.phi[:, None])
H = hat(B)
B_hat = np.dot(H, B)
assert_array_almost_equal(B, B_hat)
R = lcr_matrix(H)
d = np.arange(len(hemi.theta))
r = d - np.dot(H, d)
lev = np.sqrt(1 - H.diagonal())
r /= lev
r -= r.mean()
r2 = np.dot(R, d)
assert_array_almost_equal(r, r2)
r3 = np.dot(d, R.T)
assert_array_almost_equal(r, r3)
```

## Next Steps


---

*Source: test_shm.py:682 | Complexity: Advanced | Last updated: 2026-05-18*