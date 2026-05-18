# How To: Fss Radius Search

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fss radius search

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.segment.fss`
- `dipy.segment.metric`
- `dipy.testing`


## Step-by-Step Guide

### Step 1: Assign r = 4.0

```python
r = 4.0
```

**Verification:**
```python
assert_greater(rs_f2_in_f1.nnz, 0)
```

### Step 2: Assign nb_pts = 24

```python
nb_pts = 24
```

**Verification:**
```python
assert_greater(rs_f1_in_f2.nnz, 0)
```

### Step 3: Assign fss_f1 = FastStreamlineSearch(...)

```python
fss_f1 = FastStreamlineSearch(f1, max_radius=r, nb_mpts=2, bin_size=20.0, resampling=nb_pts, bidirectional=True)
```

**Verification:**
```python
assert_true(rs_f2_in_f1.nnz == rs_f1_in_f2.nnz)
```

### Step 4: Assign rs_f2_in_f1 = fss_f1.radius_search(...)

```python
rs_f2_in_f1 = fss_f1.radius_search(f2, radius=r, use_negative=True)
```

**Verification:**
```python
assert_arrays_equal(np.sort(rs_f2_in_f1.row), np.sort(rs_f1_in_f2.col))
```

### Step 5: Assign fss_f2 = FastStreamlineSearch(...)

```python
fss_f2 = FastStreamlineSearch(f2, max_radius=r, nb_mpts=8, bin_size=10.0, resampling=nb_pts, bidirectional=True)
```

**Verification:**
```python
assert_arrays_equal(np.sort(rs_f2_in_f1.col), np.sort(rs_f1_in_f2.row))
```

### Step 6: Assign rs_f1_in_f2 = fss_f2.radius_search(...)

```python
rs_f1_in_f2 = fss_f2.radius_search(f1, radius=r, use_negative=False)
```

**Verification:**
```python
assert_almost_equal(np.sort(np.abs(rs_f2_in_f1.data)), np.sort(rs_f1_in_f2.data))
```

### Step 7: Call assert_greater()

```python
assert_greater(rs_f2_in_f1.nnz, 0)
```

**Verification:**
```python
assert_arrays_equal(r1_a, r2_a)
```

### Step 8: Call assert_greater()

```python
assert_greater(rs_f1_in_f2.nnz, 0)
```

**Verification:**
```python
assert_arrays_equal(r1_b, r2_b)
```

### Step 9: Call assert_true()

```python
assert_true(rs_f2_in_f1.nnz == rs_f1_in_f2.nnz)
```

**Verification:**
```python
assert_arrays_equal(r1_d, r2_d)
```

### Step 10: Call assert_arrays_equal()

```python
assert_arrays_equal(np.sort(rs_f2_in_f1.row), np.sort(rs_f1_in_f2.col))
```

**Verification:**
```python
assert_arrays_equal(r3_a, r4_a)
```

### Step 11: Call assert_arrays_equal()

```python
assert_arrays_equal(np.sort(rs_f2_in_f1.col), np.sort(rs_f1_in_f2.row))
```

**Verification:**
```python
assert_arrays_equal(r3_b, r4_b)
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(np.sort(np.abs(rs_f2_in_f1.data)), np.sort(rs_f1_in_f2.data))
```

**Verification:**
```python
assert_almost_equal(r3_d, r4_d)
```

### Step 13: Assign unknown = nearest_from_matrix_row(...)

```python
r1_a, r1_b, r1_d = nearest_from_matrix_row(rs_f2_in_f1)
```

**Verification:**
```python
assert_greater_equal(rs_f1_in_f2.nnz, rs_f1_sd.nnz)
```

### Step 14: Assign unknown = nearest_from_matrix_col(...)

```python
r2_a, r2_b, r2_d = nearest_from_matrix_col(rs_f1_in_f2)
```

**Verification:**
```python
assert_true(np.all(np.isin(rs_f1_sd.row, rs_f2_in_f1.row)))
```

### Step 15: Call assert_arrays_equal()

```python
assert_arrays_equal(r1_a, r2_a)
```

**Verification:**
```python
assert_true(np.all(np.isin(rs_f1_sd.col, rs_f2_in_f1.col)))
```

### Step 16: Call assert_arrays_equal()

```python
assert_arrays_equal(r1_b, r2_b)
```

### Step 17: Call assert_arrays_equal()

```python
assert_arrays_equal(r1_d, r2_d)
```

### Step 18: Assign unknown = nearest_from_matrix_col(...)

```python
r3_a, r3_b, r3_d = nearest_from_matrix_col(rs_f2_in_f1)
```

### Step 19: Assign unknown = nearest_from_matrix_row(...)

```python
r4_a, r4_b, r4_d = nearest_from_matrix_row(rs_f1_in_f2)
```

### Step 20: Call assert_arrays_equal()

```python
assert_arrays_equal(r3_a, r4_a)
```

### Step 21: Call assert_arrays_equal()

```python
assert_arrays_equal(r3_b, r4_b)
```

### Step 22: Call assert_almost_equal()

```python
assert_almost_equal(r3_d, r4_d)
```

### Step 23: Assign fss_sd = FastStreamlineSearch(...)

```python
fss_sd = FastStreamlineSearch(f1, max_radius=r, nb_mpts=6, bin_size=80.0, resampling=nb_pts, bidirectional=False)
```

### Step 24: Assign rs_f1_sd = fss_sd.radius_search(...)

```python
rs_f1_sd = fss_sd.radius_search(f2, radius=r, use_negative=True)
```

### Step 25: Call assert_greater_equal()

```python
assert_greater_equal(rs_f1_in_f2.nnz, rs_f1_sd.nnz)
```

### Step 26: Call assert_true()

```python
assert_true(np.all(np.isin(rs_f1_sd.row, rs_f2_in_f1.row)))
```

### Step 27: Call assert_true()

```python
assert_true(np.all(np.isin(rs_f1_sd.col, rs_f2_in_f1.col)))
```


## Complete Example

```python
# Workflow
r = 4.0
nb_pts = 24
fss_f1 = FastStreamlineSearch(f1, max_radius=r, nb_mpts=2, bin_size=20.0, resampling=nb_pts, bidirectional=True)
rs_f2_in_f1 = fss_f1.radius_search(f2, radius=r, use_negative=True)
fss_f2 = FastStreamlineSearch(f2, max_radius=r, nb_mpts=8, bin_size=10.0, resampling=nb_pts, bidirectional=True)
rs_f1_in_f2 = fss_f2.radius_search(f1, radius=r, use_negative=False)
assert_greater(rs_f2_in_f1.nnz, 0)
assert_greater(rs_f1_in_f2.nnz, 0)
assert_true(rs_f2_in_f1.nnz == rs_f1_in_f2.nnz)
assert_arrays_equal(np.sort(rs_f2_in_f1.row), np.sort(rs_f1_in_f2.col))
assert_arrays_equal(np.sort(rs_f2_in_f1.col), np.sort(rs_f1_in_f2.row))
assert_almost_equal(np.sort(np.abs(rs_f2_in_f1.data)), np.sort(rs_f1_in_f2.data))
r1_a, r1_b, r1_d = nearest_from_matrix_row(rs_f2_in_f1)
r2_a, r2_b, r2_d = nearest_from_matrix_col(rs_f1_in_f2)
assert_arrays_equal(r1_a, r2_a)
assert_arrays_equal(r1_b, r2_b)
assert_arrays_equal(r1_d, r2_d)
r3_a, r3_b, r3_d = nearest_from_matrix_col(rs_f2_in_f1)
r4_a, r4_b, r4_d = nearest_from_matrix_row(rs_f1_in_f2)
assert_arrays_equal(r3_a, r4_a)
assert_arrays_equal(r3_b, r4_b)
assert_almost_equal(r3_d, r4_d)
fss_sd = FastStreamlineSearch(f1, max_radius=r, nb_mpts=6, bin_size=80.0, resampling=nb_pts, bidirectional=False)
rs_f1_sd = fss_sd.radius_search(f2, radius=r, use_negative=True)
assert_greater_equal(rs_f1_in_f2.nnz, rs_f1_sd.nnz)
assert_true(np.all(np.isin(rs_f1_sd.row, rs_f2_in_f1.row)))
assert_true(np.all(np.isin(rs_f1_sd.col, rs_f2_in_f1.col)))
```

## Next Steps


---

*Source: test_fss.py:30 | Complexity: Advanced | Last updated: 2026-05-18*