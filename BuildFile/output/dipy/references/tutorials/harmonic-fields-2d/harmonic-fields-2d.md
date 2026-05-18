# How To: Harmonic Fields 2D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test harmonic fields 2d

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

### Step 1: Assign nrows = 64

```python
nrows = 64
```

**Verification:**
```python
assert_array_almost_equal(expected_d, actual_d)
```

### Step 2: Assign ncols = 67

```python
ncols = 67
```

**Verification:**
```python
assert_array_almost_equal(expected_d_inv, expected_d_inv)
```

### Step 3: Assign mid_row = value

```python
mid_row = nrows // 2
```

### Step 4: Assign mid_col = value

```python
mid_col = ncols // 2
```

### Step 5: Assign expected_d = np.empty(...)

```python
expected_d = np.empty(shape=(nrows, ncols, 2))
```

### Step 6: Assign expected_d_inv = np.empty(...)

```python
expected_d_inv = np.empty(shape=(nrows, ncols, 2))
```

### Step 7: Assign unknown = vfu.create_harmonic_fields_2d(...)

```python
actual_d, actual_d_inv = vfu.create_harmonic_fields_2d(nrows, ncols, b, m)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(expected_d, actual_d)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(expected_d_inv, expected_d_inv)
```

### Step 10: Assign ii = value

```python
ii = i - mid_row
```

### Step 11: Assign jj = value

```python
jj = j - mid_col
```

### Step 12: Assign theta = np.arctan2(...)

```python
theta = np.arctan2(ii, jj)
```

### Step 13: Assign unknown = value

```python
expected_d[i, j, 0] = ii * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
```

### Step 14: Assign unknown = value

```python
expected_d[i, j, 1] = jj * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
```

### Step 15: Assign unknown = value

```python
expected_d_inv[i, j, 0] = b * np.cos(m * theta) * ii
```

### Step 16: Assign unknown = value

```python
expected_d_inv[i, j, 1] = b * np.cos(m * theta) * jj
```


## Complete Example

```python
# Workflow
nrows = 64
ncols = 67
mid_row = nrows // 2
mid_col = ncols // 2
expected_d = np.empty(shape=(nrows, ncols, 2))
expected_d_inv = np.empty(shape=(nrows, ncols, 2))
for b in [0.1, 0.3, 0.7]:
    for m in [2, 4, 7]:
        for i in range(nrows):
            for j in range(ncols):
                ii = i - mid_row
                jj = j - mid_col
                theta = np.arctan2(ii, jj)
                expected_d[i, j, 0] = ii * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
                expected_d[i, j, 1] = jj * (1.0 / (1 + b * np.cos(m * theta)) - 1.0)
                expected_d_inv[i, j, 0] = b * np.cos(m * theta) * ii
                expected_d_inv[i, j, 1] = b * np.cos(m * theta) * jj
        actual_d, actual_d_inv = vfu.create_harmonic_fields_2d(nrows, ncols, b, m)
        assert_array_almost_equal(expected_d, actual_d)
        assert_array_almost_equal(expected_d_inv, expected_d_inv)
```

## Next Steps


---

*Source: test_vector_fields.py:202 | Complexity: Advanced | Last updated: 2026-05-18*