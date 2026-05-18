# How To: Squared Loss Gradient At Simple Points

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test gradient of data loss function in points near to zero.

This is a not so hard test, just for detecting big errors.

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

### Step 1: 'Test gradient of data loss function in points near to zero.\n\n    This is a not so hard test, just for detecting big errors.\n    '

```python
'Test gradient of data loss function in points near to zero.\n\n    This is a not so hard test, just for detecting big errors.\n    '
```

**Verification:**
```python
assert_almost_equal(sp.optimize.check_grad(func, func_grad, point), 0, decimal=3)
```

### Step 2: Assign unknown = create_graph_net_simulation_data(...)

```python
X, y, w, mask = create_graph_net_simulation_data(n_samples=10, size=4)
```

### Step 3: Assign grad_weight = 1

```python
grad_weight = 1
```

### Step 4: Assign point = np.zeros(...)

```python
point = np.zeros(*w.shape)
```

### Step 5: Assign unknown = 1

```python
point[i] = 1
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(sp.optimize.check_grad(func, func_grad, point), 0, decimal=3)
```


## Complete Example

```python
# Workflow
'Test gradient of data loss function in points near to zero.\n\n    This is a not so hard test, just for detecting big errors.\n    '
X, y, w, mask = create_graph_net_simulation_data(n_samples=10, size=4)
grad_weight = 1

def func(w):
    return _squared_loss_and_spatial_grad(X, y, w, mask, grad_weight)

def func_grad(w):
    return _squared_loss_and_spatial_grad_derivative(X, y, w, mask, grad_weight)
for i in range(0, w.size, 2):
    point = np.zeros(*w.shape)
    point[i] = 1
    assert_almost_equal(sp.optimize.check_grad(func, func_grad, point), 0, decimal=3)
```

## Next Steps


---

*Source: test_graph_net.py:134 | Complexity: Intermediate | Last updated: 2026-05-18*