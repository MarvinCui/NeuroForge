# How To: Same Energy Calculus Pure Lasso

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test same energy calculus pure lasso

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
X, y, w, mask = _make_data(rng=rng, masked=True)
```

**Verification:**
```python
assert f1 == f2
```

### Step 2: Assign f1 = squared_loss(...)

```python
f1 = squared_loss(X, y, w)
```

**Verification:**
```python
assert_array_equal(g1, g2)
```

### Step 3: Assign f2 = _squared_loss_and_spatial_grad(...)

```python
f2 = _squared_loss_and_spatial_grad(X, y, w.ravel(), mask, 0.0)
```

**Verification:**
```python
assert f1 == f2
```

### Step 4: Assign g1 = squared_loss_grad(...)

```python
g1 = squared_loss_grad(X, y, w)
```

### Step 5: Assign g2 = _squared_loss_and_spatial_grad_derivative(...)

```python
g2 = _squared_loss_and_spatial_grad_derivative(X, y, w.ravel(), mask, 0.0)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(g1, g2)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
X, y, w, mask = _make_data(rng=rng, masked=True)
f1 = squared_loss(X, y, w)
f2 = _squared_loss_and_spatial_grad(X, y, w.ravel(), mask, 0.0)
assert f1 == f2
g1 = squared_loss_grad(X, y, w)
g2 = _squared_loss_and_spatial_grad_derivative(X, y, w.ravel(), mask, 0.0)
assert_array_equal(g1, g2)
```

## Next Steps


---

*Source: test_same_api.py:79 | Complexity: Intermediate | Last updated: 2026-05-18*