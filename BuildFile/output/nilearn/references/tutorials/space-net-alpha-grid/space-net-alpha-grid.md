# How To: Space Net Alpha Grid

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test space net alpha grid

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `sklearn.datasets`
- `sklearn.linear_model`
- `sklearn.linear_model._coordinate_descent`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.decoding._utils`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.decoding.tests._testing`
- `nilearn.decoding.tests.test_same_api`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng, is_classif, l1_ratio, n_alphas, n_samples, n_features
```

## Step-by-Step Guide

### Step 1: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal((n_samples, n_features))
```

**Verification:**
```python
assert_almost_equal(_space_net_alpha_grid(X, y, n_alphas=n_alphas, l1_ratio=l1_ratio, logistic=is_classif), alpha_max)
```

### Step 2: Assign y = np.arange(...)

```python
y = np.arange(n_samples)
```

**Verification:**
```python
assert_almost_equal(alphas.max(), alpha_max)
```

### Step 3: Assign alpha_max = value

```python
alpha_max = np.max(np.abs(np.dot(X.T, y))) / l1_ratio
```

**Verification:**
```python
assert_almost_equal(n_alphas, len(alphas))
```

### Step 4: Assign alphas = _space_net_alpha_grid(...)

```python
alphas = _space_net_alpha_grid(X, y, n_alphas=n_alphas, l1_ratio=l1_ratio, logistic=is_classif)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(alphas.max(), alpha_max)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(n_alphas, len(alphas))
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(_space_net_alpha_grid(X, y, n_alphas=n_alphas, l1_ratio=l1_ratio, logistic=is_classif), alpha_max)
```


## Complete Example

```python
# Setup
# Fixtures: rng, is_classif, l1_ratio, n_alphas, n_samples, n_features

# Workflow
X = rng.standard_normal((n_samples, n_features))
y = np.arange(n_samples)
alpha_max = np.max(np.abs(np.dot(X.T, y))) / l1_ratio
if n_alphas == 1:
    assert_almost_equal(_space_net_alpha_grid(X, y, n_alphas=n_alphas, l1_ratio=l1_ratio, logistic=is_classif), alpha_max)
alphas = _space_net_alpha_grid(X, y, n_alphas=n_alphas, l1_ratio=l1_ratio, logistic=is_classif)
assert_almost_equal(alphas.max(), alpha_max)
assert_almost_equal(n_alphas, len(alphas))
```

## Next Steps


---

*Source: test_space_net.py:93 | Complexity: Intermediate | Last updated: 2026-05-18*