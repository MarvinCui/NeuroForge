# How To: Operators Adjointness

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Perform same as test_identity_adjointness with generic design matrix.

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
# Fixtures: rng, size
```

## Step-by-Step Guide

### Step 1: 'Perform same as test_identity_adjointness with generic design matrix.'

```python
'Perform same as test_identity_adjointness with generic design matrix.'
```

**Verification:**
```python
assert_almost_equal(Axdoty, xdotAty)
```

### Step 2: Assign mask = np.ones(...)

```python
mask = np.ones((size, size, size), dtype=bool)
```

### Step 3: Assign unknown = 0

```python
mask[0:3, 0:3, 0:3] = 0
```

### Step 4: Assign adjoint_mask = np.array(...)

```python
adjoint_mask = np.array([mask for _ in range(mask.ndim)])
```

### Step 5: Assign n_samples = 200

```python
n_samples = 200
```

### Step 6: Assign X = rng.random(...)

```python
X = rng.random((n_samples, np.sum(mask)))
```

### Step 7: Assign l1_ratio = 0.5

```python
l1_ratio = 0.5
```

### Step 8: Assign x = rng.random(...)

```python
x = rng.random(np.sum(mask))
```

### Step 9: Assign y = rng.random(...)

```python
y = rng.random(n_samples + np.sum(mask) * mask.ndim)
```

### Step 10: Assign Axdoty = np.dot(...)

```python
Axdoty = np.dot(_graph_net_data_function(X, x, mask, l1_ratio), y)
```

### Step 11: Assign xdotAty = np.dot(...)

```python
xdotAty = np.dot(_graph_net_adjoint_data_function(X, y, adjoint_mask, l1_ratio), x)
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(Axdoty, xdotAty)
```


## Complete Example

```python
# Setup
# Fixtures: rng, size

# Workflow
'Perform same as test_identity_adjointness with generic design matrix.'
mask = np.ones((size, size, size), dtype=bool)
mask[0:3, 0:3, 0:3] = 0
adjoint_mask = np.array([mask for _ in range(mask.ndim)])
n_samples = 200
X = rng.random((n_samples, np.sum(mask)))
l1_ratio = 0.5
for _ in range(10):
    x = rng.random(np.sum(mask))
    y = rng.random(n_samples + np.sum(mask) * mask.ndim)
    Axdoty = np.dot(_graph_net_data_function(X, x, mask, l1_ratio), y)
    xdotAty = np.dot(_graph_net_adjoint_data_function(X, y, adjoint_mask, l1_ratio), x)
    assert_almost_equal(Axdoty, xdotAty)
```

## Next Steps


---

*Source: test_graph_net.py:112 | Complexity: Advanced | Last updated: 2026-05-18*