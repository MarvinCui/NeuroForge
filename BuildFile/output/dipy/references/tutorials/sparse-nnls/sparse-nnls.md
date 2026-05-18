# How To: Sparse Nnls

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sparse nnls

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

### Step 1: Assign beta = rng.random(...)

```python
beta = rng.random(10)
```

### Step 2: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal((1000, 10))
```

### Step 3: Assign y = np.dot(...)

```python
y = np.dot(X, beta)
```

### Step 4: Assign beta_hat = sparse_nnls(...)

```python
beta_hat = sparse_nnls(y, X)
```

### Step 5: Assign beta_hat_sparse = sparse_nnls(...)

```python
beta_hat_sparse = sparse_nnls(y, sps.csr_matrix(X))
```

### Step 6: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(beta, beta_hat, decimal=1)
```

### Step 7: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(beta, beta_hat_sparse, decimal=1)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
beta = rng.random(10)
X = rng.standard_normal((1000, 10))
y = np.dot(X, beta)
beta_hat = sparse_nnls(y, X)
beta_hat_sparse = sparse_nnls(y, sps.csr_matrix(X))
npt.assert_array_almost_equal(beta, beta_hat, decimal=1)
npt.assert_array_almost_equal(beta, beta_hat_sparse, decimal=1)
```

## Next Steps


---

*Source: test_optimize.py:116 | Complexity: Intermediate | Last updated: 2026-05-18*