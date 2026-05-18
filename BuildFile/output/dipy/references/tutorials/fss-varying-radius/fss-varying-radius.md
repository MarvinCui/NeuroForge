# How To: Fss Varying Radius

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fss varying radius

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

### Step 1: Assign fss = FastStreamlineSearch(...)

```python
fss = FastStreamlineSearch(f1, max_radius=10.0, nb_mpts=5, bin_size=20.0, resampling=25, bidirectional=True)
```

**Verification:**
```python
assert_greater_equal(rs_6.nnz, rs_4.nnz)
```

### Step 2: Assign rs_6 = fss.radius_search(...)

```python
rs_6 = fss.radius_search(f2, radius=6.0, use_negative=True)
```

**Verification:**
```python
assert_true(np.all(np.isin(rs_4.row, rs_6.row)))
```

### Step 3: Assign rs_4 = fss.radius_search(...)

```python
rs_4 = fss.radius_search(f2, radius=4.0, use_negative=True)
```

**Verification:**
```python
assert_true(np.all(np.isin(rs_4.col, rs_6.col)))
```

### Step 4: Assign rs_2 = fss.radius_search(...)

```python
rs_2 = fss.radius_search(f2, radius=2.0, use_negative=True)
```

**Verification:**
```python
assert_greater_equal(rs_4.nnz, rs_2.nnz)
```

### Step 5: Call assert_greater_equal()

```python
assert_greater_equal(rs_6.nnz, rs_4.nnz)
```

**Verification:**
```python
assert_true(np.all(np.isin(rs_2.row, rs_4.row)))
```

### Step 6: Call assert_true()

```python
assert_true(np.all(np.isin(rs_4.row, rs_6.row)))
```

**Verification:**
```python
assert_true(np.all(np.isin(rs_2.col, rs_4.col)))
```

### Step 7: Call assert_true()

```python
assert_true(np.all(np.isin(rs_4.col, rs_6.col)))
```

### Step 8: Call assert_greater_equal()

```python
assert_greater_equal(rs_4.nnz, rs_2.nnz)
```

### Step 9: Call assert_true()

```python
assert_true(np.all(np.isin(rs_2.row, rs_4.row)))
```

### Step 10: Call assert_true()

```python
assert_true(np.all(np.isin(rs_2.col, rs_4.col)))
```


## Complete Example

```python
# Workflow
fss = FastStreamlineSearch(f1, max_radius=10.0, nb_mpts=5, bin_size=20.0, resampling=25, bidirectional=True)
rs_6 = fss.radius_search(f2, radius=6.0, use_negative=True)
rs_4 = fss.radius_search(f2, radius=4.0, use_negative=True)
rs_2 = fss.radius_search(f2, radius=2.0, use_negative=True)
assert_greater_equal(rs_6.nnz, rs_4.nnz)
assert_true(np.all(np.isin(rs_4.row, rs_6.row)))
assert_true(np.all(np.isin(rs_4.col, rs_6.col)))
assert_greater_equal(rs_4.nnz, rs_2.nnz)
assert_true(np.all(np.isin(rs_2.row, rs_4.row)))
assert_true(np.all(np.isin(rs_2.col, rs_4.col)))
```

## Next Steps


---

*Source: test_fss.py:100 | Complexity: Advanced | Last updated: 2026-05-18*