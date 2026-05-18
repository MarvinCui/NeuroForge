# How To: Mfista Solver Graph Net No L1 Term

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mfista solver graph net no l1 term

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

### Step 1: Assign w = np.zeros(...)

```python
w = np.zeros(2)
```

**Verification:**
```python
assert_almost_equal(estimate_solution, solution, decimal=4)
```

### Step 2: Assign X = np.array(...)

```python
X = np.array([[1, 0], [0, 4]])
```

### Step 3: Assign y = np.array(...)

```python
y = np.array([-10, 20])
```

### Step 4: Assign lipschitz_constant = _squared_loss_derivative_lipschitz_constant(...)

```python
lipschitz_constant = _squared_loss_derivative_lipschitz_constant(X, (np.eye(2) == 1).astype(bool), 1)
```

### Step 5: Assign unknown = mfista(...)

```python
estimate_solution, _, _ = mfista(f1_grad, f2_prox, f1, lipschitz_constant, w.size, tol=1e-08, verbose=0)
```

### Step 6: Assign solution = np.array(...)

```python
solution = np.array([-10, 5])
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(estimate_solution, solution, decimal=4)
```


## Complete Example

```python
# Workflow
w = np.zeros(2)
X = np.array([[1, 0], [0, 4]])
y = np.array([-10, 20])

def f1(w):
    return 0.5 * np.dot(np.dot(X, w) - y, np.dot(X, w) - y)

def f1_grad(w):
    return np.dot(X.T, np.dot(X, w) - y)

def f2_prox(w, step_size, *args, **kwargs):
    return (w, {'converged': True})
lipschitz_constant = _squared_loss_derivative_lipschitz_constant(X, (np.eye(2) == 1).astype(bool), 1)
estimate_solution, _, _ = mfista(f1_grad, f2_prox, f1, lipschitz_constant, w.size, tol=1e-08, verbose=0)
solution = np.array([-10, 5])
assert_almost_equal(estimate_solution, solution, decimal=4)
```

## Next Steps


---

*Source: test_graph_net.py:297 | Complexity: Intermediate | Last updated: 2026-05-18*