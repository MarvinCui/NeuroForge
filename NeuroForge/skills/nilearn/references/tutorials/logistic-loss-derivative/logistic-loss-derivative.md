# How To: Logistic Loss Derivative

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logistic loss derivative

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.optimize`
- `nilearn.decoding._objective_functions`

**Setup Required:**
```python
# Fixtures: rng, n_samples, n_features, decimal
```

## Step-by-Step Guide

### Step 1: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal((n_samples, n_features))
```

**Verification:**
```python
assert_almost_equal(check_grad(lambda w: logistic_loss(X, y, w), lambda w: logistic_loss_grad(X, y, w), w), 0.0, decimal=decimal)
```

### Step 2: Assign y = rng.standard_normal(...)

```python
y = rng.standard_normal(n_samples)
```

### Step 3: Assign n_features = value

```python
n_features = X.shape[1]
```

### Step 4: Assign w = rng.standard_normal(...)

```python
w = rng.standard_normal(n_features + 1)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(check_grad(lambda w: logistic_loss(X, y, w), lambda w: logistic_loss_grad(X, y, w), w), 0.0, decimal=decimal)
```


## Complete Example

```python
# Setup
# Fixtures: rng, n_samples, n_features, decimal

# Workflow
X = rng.standard_normal((n_samples, n_features))
y = rng.standard_normal(n_samples)
n_features = X.shape[1]
w = rng.standard_normal(n_features + 1)
assert_almost_equal(check_grad(lambda w: logistic_loss(X, y, w), lambda w: logistic_loss_grad(X, y, w), w), 0.0, decimal=decimal)
```

## Next Steps


---

*Source: test_objective_functions.py:62 | Complexity: Intermediate | Last updated: 2026-05-18*