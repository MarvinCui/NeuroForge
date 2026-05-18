# How To: Spdot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test spdot

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `scipy.sparse`
- `dipy.core.optimize`
- `dipy.core.optimize`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign n = 100

```python
n = 100
```

### Step 2: Assign m = 20

```python
m = 20
```

### Step 3: Assign k = 10

```python
k = 10
```

### Step 4: Assign A = rng.standard_normal(...)

```python
A = rng.standard_normal((n, m))
```

### Step 5: Assign B = rng.standard_normal(...)

```python
B = rng.standard_normal((m, k))
```

### Step 6: Assign A_sparse = sps.csr_matrix(...)

```python
A_sparse = sps.csr_matrix(A)
```

### Step 7: Assign B_sparse = sps.csr_matrix(...)

```python
B_sparse = sps.csr_matrix(B)
```

### Step 8: Assign dense_dot = np.dot(...)

```python
dense_dot = np.dot(A, B)
```

### Step 9: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(dense_dot, spdot(A_sparse, B_sparse).todense())
```

### Step 10: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(dense_dot, spdot(A, B_sparse))
```

### Step 11: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(dense_dot, spdot(A_sparse, B))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n = 100
m = 20
k = 10
A = rng.standard_normal((n, m))
B = rng.standard_normal((m, k))
A_sparse = sps.csr_matrix(A)
B_sparse = sps.csr_matrix(B)
dense_dot = np.dot(A, B)
npt.assert_array_almost_equal(dense_dot, spdot(A_sparse, B_sparse).todense())
npt.assert_array_almost_equal(dense_dot, spdot(A, B_sparse))
npt.assert_array_almost_equal(dense_dot, spdot(A_sparse, B))
```

## Next Steps


---

*Source: test_optimize.py:100 | Complexity: Advanced | Last updated: 2026-05-18*