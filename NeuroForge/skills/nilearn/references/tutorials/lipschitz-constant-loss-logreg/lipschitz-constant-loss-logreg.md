# How To: Lipschitz Constant Loss Logreg

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test lipschitz constant loss logreg

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
assert a == b
```

### Step 2: Assign grad_weight = value

```python
grad_weight = 0.1 * X.shape[0] * 0.0
```

### Step 3: Assign a = _logistic_derivative_lipschitz_constant(...)

```python
a = _logistic_derivative_lipschitz_constant(X, mask, grad_weight)
```

### Step 4: Assign b = logistic_loss_lipschitz_constant(...)

```python
b = logistic_loss_lipschitz_constant(X)
```

**Verification:**
```python
assert a == b
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
X, _, _, mask = _make_data(rng=rng, masked=True)
grad_weight = 0.1 * X.shape[0] * 0.0
a = _logistic_derivative_lipschitz_constant(X, mask, grad_weight)
b = logistic_loss_lipschitz_constant(X)
assert a == b
```

## Next Steps


---

*Source: test_same_api.py:109 | Complexity: Intermediate | Last updated: 2026-05-18*