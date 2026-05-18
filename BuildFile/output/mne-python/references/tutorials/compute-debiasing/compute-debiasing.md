# How To: Compute Debiasing

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test source amplitude debiasing.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `mne.inverse_sparse.mxne_debiasing`


## Step-by-Step Guide

### Step 1: 'Test source amplitude debiasing.'

```python
'Test source amplitude debiasing.'
```

**Verification:**
```python
assert_almost_equal(debias, debias_true, decimal=5)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(42)
```

**Verification:**
```python
assert_almost_equal(debias, [1.8, 1.8, 3.72, 3.72], decimal=2)
```

### Step 3: Assign G = rng.randn(...)

```python
G = rng.randn(10, 4)
```

### Step 4: Assign X = rng.randn(...)

```python
X = rng.randn(4, 20)
```

### Step 5: Assign debias_true = np.arange(...)

```python
debias_true = np.arange(1, 5, dtype=np.float64)
```

### Step 6: Assign M = np.dot(...)

```python
M = np.dot(G, X * debias_true[:, np.newaxis])
```

### Step 7: Assign debias = compute_bias(...)

```python
debias = compute_bias(M, G, X, max_iter=10000, n_orient=1, tol=1e-07)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(debias, debias_true, decimal=5)
```

### Step 9: Assign debias = compute_bias(...)

```python
debias = compute_bias(M, G, X, max_iter=10000, n_orient=2, tol=1e-05)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(debias, [1.8, 1.8, 3.72, 3.72], decimal=2)
```


## Complete Example

```python
# Workflow
'Test source amplitude debiasing.'
rng = np.random.RandomState(42)
G = rng.randn(10, 4)
X = rng.randn(4, 20)
debias_true = np.arange(1, 5, dtype=np.float64)
M = np.dot(G, X * debias_true[:, np.newaxis])
debias = compute_bias(M, G, X, max_iter=10000, n_orient=1, tol=1e-07)
assert_almost_equal(debias, debias_true, decimal=5)
debias = compute_bias(M, G, X, max_iter=10000, n_orient=2, tol=1e-05)
assert_almost_equal(debias, [1.8, 1.8, 3.72, 3.72], decimal=2)
```

## Next Steps


---

*Source: test_mxne_debiasing.py:11 | Complexity: Advanced | Last updated: 2026-05-18*