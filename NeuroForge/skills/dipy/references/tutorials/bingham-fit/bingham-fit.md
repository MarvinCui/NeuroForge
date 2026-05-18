# How To: Bingham Fit

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests for bingham function and single Bingham fit

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.bingham`
- `dipy.reconst.shm`


## Step-by-Step Guide

### Step 1: 'Tests for bingham function and single Bingham fit'

```python
'Tests for bingham function and single Bingham fit'
```

**Verification:**
```python
assert_almost_equal(odf_test, f0)
```

### Step 2: Assign peak_dir = np.array(...)

```python
peak_dir = np.array([1, 0, 0])
```

**Verification:**
```python
assert_almost_equal(a0, f0, decimal=3)
```

### Step 3: Assign ma_axis = np.array(...)

```python
ma_axis = np.array([0, 1, 0])
```

**Verification:**
```python
assert_almost_equal(c1, k1, decimal=3)
```

### Step 4: Assign mi_axis = np.array(...)

```python
mi_axis = np.array([0, 0, 1])
```

**Verification:**
```python
assert_almost_equal(c2, k2, decimal=3)
```

### Step 5: Assign k1 = 2

```python
k1 = 2
```

**Verification:**
```python
assert_array_almost_equal(np.abs(np.diag(np.dot(Mus, Mus_ref))), np.ones(3), decimal=5)
```

### Step 6: Assign k2 = 6

```python
k2 = 6
```

**Verification:**
```python
assert_almost_equal(fits[0][0], f0, decimal=3)
```

### Step 7: Assign f0 = 3

```python
f0 = 3
```

**Verification:**
```python
assert_almost_equal(fits[0][1], k1, decimal=3)
```

### Step 8: Assign odf_test = _single_bingham_to_sf(...)

```python
odf_test = _single_bingham_to_sf(f0, k1, k2, ma_axis, mi_axis, peak_dir)
```

**Verification:**
```python
assert_almost_equal(fits[0][2], k2, decimal=3)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(odf_test, f0)
```

**Verification:**
```python
assert_array_almost_equal(np.abs(np.diag(np.dot(Mus, Mus_ref))), np.ones(3), decimal=5)
```

### Step 10: Assign odf_gt = _single_bingham_to_sf(...)

```python
odf_gt = _single_bingham_to_sf(f0, k1, k2, ma_axis, mi_axis, sphere.vertices)
```

### Step 11: Assign unknown = _bingham_fit_peak(...)

```python
a0, c1, c2, mu0, mu1, mu2 = _bingham_fit_peak(odf_gt, peak_dir, sphere, 45)
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(a0, f0, decimal=3)
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(c1, k1, decimal=3)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(c2, k2, decimal=3)
```

### Step 15: Assign Mus = np.array(...)

```python
Mus = np.array([mu0, mu1, mu2])
```

### Step 16: Assign Mus_ref = np.array(...)

```python
Mus_ref = np.array([peak_dir, ma_axis, mi_axis])
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.abs(np.diag(np.dot(Mus, Mus_ref))), np.ones(3), decimal=5)
```

### Step 18: Assign unknown = _single_sf_to_bingham(...)

```python
fits, n = _single_sf_to_bingham(odf_gt, sphere, max_search_angle=45)
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(fits[0][0], f0, decimal=3)
```

### Step 20: Call assert_almost_equal()

```python
assert_almost_equal(fits[0][1], k1, decimal=3)
```

### Step 21: Call assert_almost_equal()

```python
assert_almost_equal(fits[0][2], k2, decimal=3)
```

### Step 22: Assign Mus = np.array(...)

```python
Mus = np.array([fits[0][3], fits[0][4], fits[0][5]])
```

### Step 23: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.abs(np.diag(np.dot(Mus, Mus_ref))), np.ones(3), decimal=5)
```


## Complete Example

```python
# Workflow
'Tests for bingham function and single Bingham fit'
peak_dir = np.array([1, 0, 0])
ma_axis = np.array([0, 1, 0])
mi_axis = np.array([0, 0, 1])
k1 = 2
k2 = 6
f0 = 3
odf_test = _single_bingham_to_sf(f0, k1, k2, ma_axis, mi_axis, peak_dir)
assert_almost_equal(odf_test, f0)
odf_gt = _single_bingham_to_sf(f0, k1, k2, ma_axis, mi_axis, sphere.vertices)
a0, c1, c2, mu0, mu1, mu2 = _bingham_fit_peak(odf_gt, peak_dir, sphere, 45)
assert_almost_equal(a0, f0, decimal=3)
assert_almost_equal(c1, k1, decimal=3)
assert_almost_equal(c2, k2, decimal=3)
Mus = np.array([mu0, mu1, mu2])
Mus_ref = np.array([peak_dir, ma_axis, mi_axis])
assert_array_almost_equal(np.abs(np.diag(np.dot(Mus, Mus_ref))), np.ones(3), decimal=5)
fits, n = _single_sf_to_bingham(odf_gt, sphere, max_search_angle=45)
assert_almost_equal(fits[0][0], f0, decimal=3)
assert_almost_equal(fits[0][1], k1, decimal=3)
assert_almost_equal(fits[0][2], k2, decimal=3)
Mus = np.array([fits[0][3], fits[0][4], fits[0][5]])
assert_array_almost_equal(np.abs(np.diag(np.dot(Mus, Mus_ref))), np.ones(3), decimal=5)
```

## Next Steps


---

*Source: test_bingham.py:40 | Complexity: Advanced | Last updated: 2026-05-18*