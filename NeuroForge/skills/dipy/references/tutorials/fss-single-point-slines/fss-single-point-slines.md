# How To: Fss Single Point Slines

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fss single point slines

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

### Step 1: Assign slines = value

```python
slines = [np.array([[1.0, 1.0, 1.0]]), np.array([[0.0, 1.0, 2.0]])]
```

**Verification:**
```python
assert_true(res.nnz == 4)
```

### Step 2: Assign fss = FastStreamlineSearch(...)

```python
fss = FastStreamlineSearch(slines, max_radius=4.0, nb_mpts=4, bin_size=20.0, resampling=24, bidirectional=False)
```

**Verification:**
```python
assert_almost_equal(mat[0, 0], 0.0)
```

### Step 3: Assign res = fss.radius_search(...)

```python
res = fss.radius_search(slines, radius=4.0)
```

**Verification:**
```python
assert_almost_equal(mat[1, 1], 0.0)
```

### Step 4: Call assert_true()

```python
assert_true(res.nnz == 4)
```

**Verification:**
```python
assert_almost_equal(mat[1, 0], dist)
```

### Step 5: Assign mat = res.toarray(...)

```python
mat = res.toarray()
```

**Verification:**
```python
assert_almost_equal(mat[0, 1], dist)
```

### Step 6: Assign dist = mean_euclidean_distance(...)

```python
dist = mean_euclidean_distance(slines[0], slines[1])
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(mat[0, 0], 0.0)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(mat[1, 1], 0.0)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(mat[1, 0], dist)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(mat[0, 1], dist)
```


## Complete Example

```python
# Workflow
slines = [np.array([[1.0, 1.0, 1.0]]), np.array([[0.0, 1.0, 2.0]])]
fss = FastStreamlineSearch(slines, max_radius=4.0, nb_mpts=4, bin_size=20.0, resampling=24, bidirectional=False)
res = fss.radius_search(slines, radius=4.0)
assert_true(res.nnz == 4)
mat = res.toarray()
dist = mean_euclidean_distance(slines[0], slines[1])
assert_almost_equal(mat[0, 0], 0.0)
assert_almost_equal(mat[1, 1], 0.0)
assert_almost_equal(mat[1, 0], dist)
assert_almost_equal(mat[0, 1], dist)
```

## Next Steps


---

*Source: test_fss.py:119 | Complexity: Advanced | Last updated: 2026-05-18*