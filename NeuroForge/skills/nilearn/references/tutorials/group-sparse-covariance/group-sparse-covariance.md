# How To: Group Sparse Covariance

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test group sparse covariance

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `sklearn.model_selection`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.connectome`
- `nilearn.connectome.group_sparse_cov`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = generate_group_sparse_gaussian_graphs(...)

```python
signals, _, _ = generate_group_sparse_gaussian_graphs(density=0.1, n_subjects=5, n_features=10, min_n_samples=100, max_n_samples=151, random_state=rng)
```

### Step 2: Assign alpha = 0.1

```python
alpha = 0.1
```

### Step 3: Assign unknown = group_sparse_covariance(...)

```python
_, omega = group_sparse_covariance(signals, alpha, max_iter=20, tol=0.01, debug=True, verbose=1)
```

### Step 4: Assign unknown = group_sparse_covariance(...)

```python
_, omega2 = group_sparse_covariance(signals, alpha, max_iter=20, tol=0.01, debug=True)
```

### Step 5: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(omega, omega2, decimal=4)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
signals, _, _ = generate_group_sparse_gaussian_graphs(density=0.1, n_subjects=5, n_features=10, min_n_samples=100, max_n_samples=151, random_state=rng)
alpha = 0.1
_, omega = group_sparse_covariance(signals, alpha, max_iter=20, tol=0.01, debug=True, verbose=1)
_, omega2 = group_sparse_covariance(signals, alpha, max_iter=20, tol=0.01, debug=True)
np.testing.assert_almost_equal(omega, omega2, decimal=4)
```

## Next Steps


---

*Source: test_group_sparse_cov.py:65 | Complexity: Intermediate | Last updated: 2026-05-18*