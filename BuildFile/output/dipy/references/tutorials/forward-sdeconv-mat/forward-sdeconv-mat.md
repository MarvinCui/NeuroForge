# How To: Forward Sdeconv Mat

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test forward sdeconv mat

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.gradients`
- `dipy.reconst.csdeconv`
- `dipy.reconst.dti`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign unknown = sph_harm_ind_list(...)

```python
_, l_values = sph_harm_ind_list(4)
```

### Step 2: Assign mat = forward_sdeconv_mat(...)

```python
mat = forward_sdeconv_mat(np.array([0, 2, 4]), l_values)
```

### Step 3: Assign expected = np.diag(...)

```python
expected = np.diag([0, 2, 2, 2, 2, 2, 4, 4, 4, 4, 4, 4, 4, 4, 4])
```

### Step 4: Call npt.assert_array_equal()

```python
npt.assert_array_equal(mat, expected)
```

### Step 5: Assign sh_order_max = 8

```python
sh_order_max = 8
```

### Step 6: Assign expected_size = value

```python
expected_size = (sh_order_max + 1) * (sh_order_max + 2) / 2
```

### Step 7: Assign r_rh = np.arange(...)

```python
r_rh = np.arange(0, sh_order_max + 1, 2)
```

### Step 8: Assign unknown = sph_harm_ind_list(...)

```python
m_values, l_values = sph_harm_ind_list(sh_order_max)
```

### Step 9: Assign mat = forward_sdeconv_mat(...)

```python
mat = forward_sdeconv_mat(r_rh, l_values)
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(mat.shape, (expected_size, expected_size))
```

### Step 11: Call npt.assert_array_equal()

```python
npt.assert_array_equal(mat.diagonal(), l_values)
```

### Step 12: Assign unknown = 3

```python
l_values[2] = 3
```

### Step 13: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, forward_sdeconv_mat, r_rh, l_values)
```


## Complete Example

```python
# Workflow
_, l_values = sph_harm_ind_list(4)
mat = forward_sdeconv_mat(np.array([0, 2, 4]), l_values)
expected = np.diag([0, 2, 2, 2, 2, 2, 4, 4, 4, 4, 4, 4, 4, 4, 4])
npt.assert_array_equal(mat, expected)
sh_order_max = 8
expected_size = (sh_order_max + 1) * (sh_order_max + 2) / 2
r_rh = np.arange(0, sh_order_max + 1, 2)
m_values, l_values = sph_harm_ind_list(sh_order_max)
mat = forward_sdeconv_mat(r_rh, l_values)
npt.assert_equal(mat.shape, (expected_size, expected_size))
npt.assert_array_equal(mat.diagonal(), l_values)
l_values[2] = 3
npt.assert_raises(ValueError, forward_sdeconv_mat, r_rh, l_values)
```

## Next Steps


---

*Source: test_csdeconv.py:473 | Complexity: Advanced | Last updated: 2026-05-18*