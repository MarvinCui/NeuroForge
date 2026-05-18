# How To: Lipschitz Constant Loss Mse

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test lipschitz constant loss mse

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.datasets`
- `nilearn.decoding._objective_functions`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.image`
- `nilearn.masking`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = _make_data(...)

```python
X, _, _, mask = _make_data(rng=rng, masked=True)
```

**Verification:**
```python
assert_almost_equal(a, b)
```

### Step 2: Assign alpha = 0.1

```python
alpha = 0.1
```

### Step 3: Assign mask = np.ones.astype(...)

```python
mask = np.ones(X.shape[1]).astype(bool)
```

### Step 4: Assign grad_weight = value

```python
grad_weight = alpha * X.shape[0] * 0.0
```

### Step 5: Assign a = _squared_loss_derivative_lipschitz_constant(...)

```python
a = _squared_loss_derivative_lipschitz_constant(X, mask, grad_weight)
```

### Step 6: Assign b = spectral_norm_squared(...)

```python
b = spectral_norm_squared(X)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(a, b)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
X, _, _, mask = _make_data(rng=rng, masked=True)
alpha = 0.1
mask = np.ones(X.shape[1]).astype(bool)
grad_weight = alpha * X.shape[0] * 0.0
a = _squared_loss_derivative_lipschitz_constant(X, mask, grad_weight)
b = spectral_norm_squared(X)
assert_almost_equal(a, b)
```

## Next Steps


---

*Source: test_same_api.py:96 | Complexity: Intermediate | Last updated: 2026-05-18*