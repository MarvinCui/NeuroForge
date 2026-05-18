# How To: Squared Loss Lipschitz

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test squared loss lipschitz

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.decoding._objective_functions`
- `nilearn.decoding._proximal_operators`
- `nilearn.decoding.fista`

**Setup Required:**
```python
# Fixtures: rng, scaling, n_samples, n_features
```

## Step-by-Step Guide

### Step 1: Assign X = value

```python
X = rng.standard_normal((n_samples, n_features)) * scaling
```

### Step 2: Assign y = rng.standard_normal(...)

```python
y = rng.standard_normal(n_samples)
```

### Step 3: Assign n_features = value

```python
n_features = X.shape[1]
```

### Step 4: Assign L = spectral_norm_squared(...)

```python
L = spectral_norm_squared(X)
```

### Step 5: Call _check_lipschitz_continuous()

```python
_check_lipschitz_continuous(lambda w: squared_loss_grad(X, y, w), n_features, L)
```


## Complete Example

```python
# Setup
# Fixtures: rng, scaling, n_samples, n_features

# Workflow
X = rng.standard_normal((n_samples, n_features)) * scaling
y = rng.standard_normal(n_samples)
n_features = X.shape[1]
L = spectral_norm_squared(X)
_check_lipschitz_continuous(lambda w: squared_loss_grad(X, y, w), n_features, L)
```

## Next Steps


---

*Source: test_fista.py:29 | Complexity: Intermediate | Last updated: 2026-05-18*