# How To: Squared Loss Derivative Lipschitz Constant

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Lipschitz-continuity of the derivative of squared_loss loss     function.
    

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test Lipschitz-continuity of the derivative of squared_loss loss     function.\n    '

```python
'Test Lipschitz-continuity of the derivative of squared_loss loss     function.\n    '
```

**Verification:**
```python
assert gradient_difference <= lipschitz_constant * point_difference
```

### Step 2: Assign unknown = _make_data(...)

```python
X, y, w, mask, *_ = _make_data()
```

### Step 3: Assign grad_weight = 0.208

```python
grad_weight = 0.208
```

### Step 4: Assign lipschitz_constant = _squared_loss_derivative_lipschitz_constant(...)

```python
lipschitz_constant = _squared_loss_derivative_lipschitz_constant(X, mask, grad_weight)
```

### Step 5: Assign x_1 = value

```python
x_1 = rng.random(w.shape) * rng.integers(1000)
```

### Step 6: Assign x_2 = value

```python
x_2 = rng.random(w.shape) * rng.integers(1000)
```

### Step 7: Assign gradient_difference = linalg.norm(...)

```python
gradient_difference = linalg.norm(_squared_loss_and_spatial_grad_derivative(X, y, x_1, mask, grad_weight) - _squared_loss_and_spatial_grad_derivative(X, y, x_2, mask, grad_weight))
```

### Step 8: Assign point_difference = linalg.norm(...)

```python
point_difference = linalg.norm(x_1 - x_2)
```

**Verification:**
```python
assert gradient_difference <= lipschitz_constant * point_difference
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test Lipschitz-continuity of the derivative of squared_loss loss     function.\n    '
X, y, w, mask, *_ = _make_data()
grad_weight = 0.208
lipschitz_constant = _squared_loss_derivative_lipschitz_constant(X, mask, grad_weight)
for _ in range(20):
    x_1 = rng.random(w.shape) * rng.integers(1000)
    x_2 = rng.random(w.shape) * rng.integers(1000)
    gradient_difference = linalg.norm(_squared_loss_and_spatial_grad_derivative(X, y, x_1, mask, grad_weight) - _squared_loss_and_spatial_grad_derivative(X, y, x_2, mask, grad_weight))
    point_difference = linalg.norm(x_1 - x_2)
    assert gradient_difference <= lipschitz_constant * point_difference
```

## Next Steps


---

*Source: test_graph_net.py:186 | Complexity: Advanced | Last updated: 2026-05-18*