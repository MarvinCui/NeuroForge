# How To: Tikhonov Regularization Vs Graph Net

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test one of the extreme cases of Graph-Net.

That is, with l1_ratio = 0 (pure Smooth),
we compare Graph-Net's performance
with the analytical solution for Tikhonov Regularization.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `scipy`
- `nibabel`
- `numpy.testing`
- `scipy`
- `nilearn.decoding._objective_functions`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.decoding.tests._testing`
- `test_same_api`


## Step-by-Step Guide

### Step 1: "Test one of the extreme cases of Graph-Net.\n\n    That is, with l1_ratio = 0 (pure Smooth),\n    we compare Graph-Net's performance\n    with the analytical solution for Tikhonov Regularization.\n    "

```python
"Test one of the extreme cases of Graph-Net.\n\n    That is, with l1_ratio = 0 (pure Smooth),\n    we compare Graph-Net's performance\n    with the analytical solution for Tikhonov Regularization.\n    "
```

**Verification:**
```python
assert_almost_equal(graph_net_perf, optimal_model_perf, decimal=1)
```

### Step 2: Assign unknown = _make_data(...)

```python
X, y, w, mask, mask_, X_ = _make_data()
```

### Step 3: Assign G = get_gradient_matrix(...)

```python
G = get_gradient_matrix(w.size, mask)
```

### Step 4: Assign optimal_model = np.dot(...)

```python
optimal_model = np.dot(sp.linalg.pinv(np.dot(X.T, X) + y.size * np.dot(G.T, G)), np.dot(X.T, y))
```

### Step 5: Assign graph_net = SpaceNetRegressor(...)

```python
graph_net = SpaceNetRegressor(mask=mask_, alphas=1.0 * X.shape[0], l1_ratios=0.0, max_iter=400, fit_intercept=False, screening_percentile=100.0, standardize=False)
```

### Step 6: Call graph_net.fit()

```python
graph_net.fit(X_, y.copy())
```

### Step 7: Assign coef_ = value

```python
coef_ = graph_net.coef_[0]
```

### Step 8: Assign graph_net_perf = value

```python
graph_net_perf = 0.5 / y.size * linalg.norm(np.dot(X, coef_) - y) ** 2 + 0.5 * linalg.norm(np.dot(G, coef_)) ** 2
```

### Step 9: Assign optimal_model_perf = value

```python
optimal_model_perf = 0.5 / y.size * linalg.norm(np.dot(X, optimal_model) - y) ** 2 + 0.5 * linalg.norm(np.dot(G, optimal_model)) ** 2
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(graph_net_perf, optimal_model_perf, decimal=1)
```


## Complete Example

```python
# Workflow
"Test one of the extreme cases of Graph-Net.\n\n    That is, with l1_ratio = 0 (pure Smooth),\n    we compare Graph-Net's performance\n    with the analytical solution for Tikhonov Regularization.\n    "
X, y, w, mask, mask_, X_ = _make_data()
G = get_gradient_matrix(w.size, mask)
optimal_model = np.dot(sp.linalg.pinv(np.dot(X.T, X) + y.size * np.dot(G.T, G)), np.dot(X.T, y))
graph_net = SpaceNetRegressor(mask=mask_, alphas=1.0 * X.shape[0], l1_ratios=0.0, max_iter=400, fit_intercept=False, screening_percentile=100.0, standardize=False)
graph_net.fit(X_, y.copy())
coef_ = graph_net.coef_[0]
graph_net_perf = 0.5 / y.size * linalg.norm(np.dot(X, coef_) - y) ** 2 + 0.5 * linalg.norm(np.dot(G, coef_)) ** 2
optimal_model_perf = 0.5 / y.size * linalg.norm(np.dot(X, optimal_model) - y) ** 2 + 0.5 * linalg.norm(np.dot(G, optimal_model)) ** 2
assert_almost_equal(graph_net_perf, optimal_model_perf, decimal=1)
```

## Next Steps


---

*Source: test_graph_net.py:259 | Complexity: Advanced | Last updated: 2026-05-18*