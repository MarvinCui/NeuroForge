# How To: Geometric Mean Properties Check Gradient

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test geometric mean properties check gradient

## Prerequisites

**Required Modules:**
- `copy`
- `warnings`
- `math`
- `numpy`
- `pytest`
- `numpy.testing`
- `pandas`
- `scipy`
- `sklearn.covariance`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.extmath`
- `nilearn._utils.versions`
- `nilearn.connectome.connectivity_matrices`
- `nilearn.tests.test_signal`


## Step-by-Step Guide

### Step 1: Assign n_matrices = 40

```python
n_matrices = 40
```

**Verification:**
```python
assert np.amax(difference) <= 0.0
```

### Step 2: Assign n_features = 15

```python
n_features = 15
```

**Verification:**
```python
assert len(w) == 1
```

### Step 3: Assign spds = value

```python
spds = [random_spd(n_features, eig_min=1.0, cond=10.0, random_state=0) for _ in range(n_matrices)]
```

**Verification:**
```python
assert len(grad_norm) == max_iter
```

### Step 4: Assign grad_norm = grad_geometric_mean(...)

```python
grad_norm = grad_geometric_mean(spds, tol=1e-20)
```

**Verification:**
```python
assert grad_norm[-1] > tol
```

### Step 5: Assign difference = np.diff(...)

```python
difference = np.diff(grad_norm)
```

**Verification:**
```python
assert np.amax(difference) <= 0.0
```

### Step 6: Assign max_iter = 1

```python
max_iter = 1
```

### Step 7: Assign tol = 1e-20

```python
tol = 1e-20
```

### Step 8: Assign grad_norm = grad_geometric_mean(...)

```python
grad_norm = grad_geometric_mean(spds, max_iter=max_iter, tol=tol)
```

**Verification:**
```python
assert len(grad_norm) == max_iter
```

### Step 9: Call warnings.simplefilter()

```python
warnings.simplefilter('always')
```

### Step 10: Call _geometric_mean()

```python
_geometric_mean(spds, max_iter=max_iter, tol=tol)
```

**Verification:**
```python
assert len(w) == 1
```


## Complete Example

```python
# Workflow
n_matrices = 40
n_features = 15
spds = [random_spd(n_features, eig_min=1.0, cond=10.0, random_state=0) for _ in range(n_matrices)]
grad_norm = grad_geometric_mean(spds, tol=1e-20)
difference = np.diff(grad_norm)
assert np.amax(difference) <= 0.0
max_iter = 1
tol = 1e-20
with warnings.catch_warnings(record=True) as w:
    warnings.simplefilter('always')
    _geometric_mean(spds, max_iter=max_iter, tol=tol)
    assert len(w) == 1
grad_norm = grad_geometric_mean(spds, max_iter=max_iter, tol=tol)
assert len(grad_norm) == max_iter
assert grad_norm[-1] > tol
```

## Next Steps


---

*Source: test_connectivity_matrices.py:441 | Complexity: Advanced | Last updated: 2026-05-18*