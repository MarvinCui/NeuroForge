# How To: Harmonic Fields 3D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test harmonic fields 3d

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

### Step 1: Assign nslices = 25

```python
nslices = 25
```

**Verification:**
```python
assert_array_almost_equal(expected_d, actual_d)
```

### Step 2: Assign nrows = 34

```python
nrows = 34
```

**Verification:**
```python
assert_array_almost_equal(expected_d_inv, expected_d_inv)
```

### Step 3: Assign ncols = 37

```python
ncols = 37
```

### Step 4: Assign mid_slice = value

```python
mid_slice = nslices // 2
```

### Step 5: Assign mid_row = value

```python
mid_row = nrows // 2
```

### Step 6: Assign mid_col = value

```python
mid_col = ncols // 2
```

### Step 7: Assign expected_d = np.empty(...)

```python
expected_d = np.empty(shape=(nslices, nrows, ncols, 3))
```

### Step 8: Assign expected_d_inv = np.empty(...)

```python
expected_d_inv = np.empty(shape=(nslices, nrows, ncols, 3))
```

### Step 9: Assign unknown = vfu.create_harmonic_fields_3d(...)

```python
actual_d, actual_d_inv = vfu.create_harmonic_fields_3d(nslices, nrows, ncols, b, m)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(expected_d, actual_d)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(expected_d_inv, expected_d_inv)
```

### Step 12: Assign kk = value

```python
kk = k - mid_slice
```

### Step 13: Assign ii = value

```python
ii = i - mid_row
```

### Step 14: Assign jj = value

```python
jj = j - mid_col
```

### Step 15: Assign theta = np.arctan2(...)

```python
theta = np.arctan2(ii, jj)
```

### Step 16: Assign unknown = value

```python
expected_d[k, i, j, 0] = kk * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
```

### Step 17: Assign unknown = value

```python
expected_d[k, i, j, 1] = ii * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
```

### Step 18: Assign unknown = value

```python
expected_d[k, i, j, 2] = jj * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
```

### Step 19: Assign unknown = value

```python
expected_d_inv[k, i, j, 0] = b * np.cos(m * theta) * kk
```

### Step 20: Assign unknown = value

```python
expected_d_inv[k, i, j, 1] = b * np.cos(m * theta) * ii
```

### Step 21: Assign unknown = value

```python
expected_d_inv[k, i, j, 2] = b * np.cos(m * theta) * jj
```


## Complete Example

```python
# Workflow
nslices = 25
nrows = 34
ncols = 37
mid_slice = nslices // 2
mid_row = nrows // 2
mid_col = ncols // 2
expected_d = np.empty(shape=(nslices, nrows, ncols, 3))
expected_d_inv = np.empty(shape=(nslices, nrows, ncols, 3))
for b in [0.3, 0.7]:
    for m in [2, 5]:
        for k in range(nslices):
            for i in range(nrows):
                for j in range(ncols):
                    kk = k - mid_slice
                    ii = i - mid_row
                    jj = j - mid_col
                    theta = np.arctan2(ii, jj)
                    expected_d[k, i, j, 0] = kk * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
                    expected_d[k, i, j, 1] = ii * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
                    expected_d[k, i, j, 2] = jj * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
                    expected_d_inv[k, i, j, 0] = b * np.cos(m * theta) * kk
                    expected_d_inv[k, i, j, 1] = b * np.cos(m * theta) * ii
                    expected_d_inv[k, i, j, 2] = b * np.cos(m * theta) * jj
        actual_d, actual_d_inv = vfu.create_harmonic_fields_3d(nslices, nrows, ncols, b, m)
        assert_array_almost_equal(expected_d, actual_d)
        assert_array_almost_equal(expected_d_inv, expected_d_inv)
```

## Next Steps


---

*Source: test_vector_fields.py:226 | Complexity: Advanced | Last updated: 2026-05-18*