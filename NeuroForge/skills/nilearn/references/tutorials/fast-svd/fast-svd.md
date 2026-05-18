# How To: Fast Svd

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test fast singular value decomposition.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `nilearn.conftest`
- `nilearn.decomposition._base`
- `nilearn.decomposition.tests.conftest`

**Setup Required:**
```python
# Fixtures: n_features
```

## Step-by-Step Guide

### Step 1: 'Test fast singular value decomposition.'

```python
'Test fast singular value decomposition.'
```

**Verification:**
```python
assert X.shape == (n_samples, n_features)
```

### Step 2: Assign n_samples = 100

```python
n_samples = 100
```

**Verification:**
```python
assert Vr.shape == (k, n_features)
```

### Step 3: Assign k = 10

```python
k = 10
```

**Verification:**
```python
assert Ur.shape == (n_samples, k)
```

### Step 4: Assign U = _rng.normal(...)

```python
U = _rng().normal(size=(n_samples, k))
```

**Verification:**
```python
assert_array_almost_equal(np.abs(np.diag(np.corrcoef(V_[:k], Vr)))[:k], np.ones(k))
```

### Step 5: Assign V = _rng.normal(...)

```python
V = _rng().normal(size=(k, n_features))
```

### Step 6: Assign X = np.dot(...)

```python
X = np.dot(U, V)
```

**Verification:**
```python
assert X.shape == (n_samples, n_features)
```

### Step 7: Assign unknown = linalg.svd(...)

```python
_, _, V_ = linalg.svd(X, full_matrices=False)
```

### Step 8: Assign unknown = _fast_svd(...)

```python
Ur, _, Vr = _fast_svd(X, k, random_state=0)
```

**Verification:**
```python
assert Vr.shape == (k, n_features)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.abs(np.diag(np.corrcoef(V_[:k], Vr)))[:k], np.ones(k))
```


## Complete Example

```python
# Setup
# Fixtures: n_features

# Workflow
'Test fast singular value decomposition.'
n_samples = 100
k = 10
U = _rng().normal(size=(n_samples, k))
V = _rng().normal(size=(k, n_features))
X = np.dot(U, V)
assert X.shape == (n_samples, n_features)
_, _, V_ = linalg.svd(X, full_matrices=False)
Ur, _, Vr = _fast_svd(X, k, random_state=0)
assert Vr.shape == (k, n_features)
assert Ur.shape == (n_samples, k)
assert_array_almost_equal(np.abs(np.diag(np.corrcoef(V_[:k], Vr)))[:k], np.ones(k))
```

## Next Steps


---

*Source: test_base.py:17 | Complexity: Advanced | Last updated: 2026-05-18*