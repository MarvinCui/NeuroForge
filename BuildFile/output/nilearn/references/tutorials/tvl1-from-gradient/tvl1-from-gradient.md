# How To: Tvl1 From Gradient

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that _tvl1_objective.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.decoding._objective_functions`
- `nilearn.decoding.space_net_solvers`

**Setup Required:**
```python
# Fixtures: rng, alpha, l1_ratio, size, n_samples
```

## Step-by-Step Guide

### Step 1: 'Check that _tvl1_objective.'

```python
'Check that _tvl1_objective.'
```

**Verification:**
```python
assert _tvl1_objective(X, y, w.copy().ravel(), alpha, l1_ratio, mask) == squared_loss(X, y, w.copy().ravel(), compute_grad=False) + alpha * _tvl1_objective_from_gradient(gradid)
```

### Step 2: Assign shape = value

```python
shape = [size] * 3
```

### Step 3: Assign n_voxels = np.prod(...)

```python
n_voxels = np.prod(shape)
```

### Step 4: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal((n_samples, n_voxels))
```

### Step 5: Assign y = rng.standard_normal(...)

```python
y = rng.standard_normal(n_samples)
```

### Step 6: Assign w = rng.standard_normal(...)

```python
w = rng.standard_normal(shape)
```

### Step 7: Assign mask = np.ones_like.astype(...)

```python
mask = np.ones_like(w).astype(bool)
```

### Step 8: Assign gradid = gradient_id(...)

```python
gradid = gradient_id(w, l1_ratio=l1_ratio)
```

**Verification:**
```python
assert _tvl1_objective(X, y, w.copy().ravel(), alpha, l1_ratio, mask) == squared_loss(X, y, w.copy().ravel(), compute_grad=False) + alpha * _tvl1_objective_from_gradient(gradid)
```


## Complete Example

```python
# Setup
# Fixtures: rng, alpha, l1_ratio, size, n_samples

# Workflow
'Check that _tvl1_objective.'
shape = [size] * 3
n_voxels = np.prod(shape)
X = rng.standard_normal((n_samples, n_voxels))
y = rng.standard_normal(n_samples)
w = rng.standard_normal(shape)
mask = np.ones_like(w).astype(bool)
gradid = gradient_id(w, l1_ratio=l1_ratio)
assert _tvl1_objective(X, y, w.copy().ravel(), alpha, l1_ratio, mask) == squared_loss(X, y, w.copy().ravel(), compute_grad=False) + alpha * _tvl1_objective_from_gradient(gradid)
```

## Next Steps


---

*Source: test_tv.py:14 | Complexity: Advanced | Last updated: 2026-05-18*