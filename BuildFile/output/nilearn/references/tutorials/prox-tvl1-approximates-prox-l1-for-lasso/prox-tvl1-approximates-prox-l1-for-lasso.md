# How To: Prox Tvl1 Approximates Prox L1 For Lasso

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test prox tvl1 approximates prox l1 for lasso

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.decoding._proximal_operators`

**Setup Required:**
```python
# Fixtures: rng, ndim, weight, size, decimal, dgap_tol
```

## Step-by-Step Guide

### Step 1: Assign l1_ratio = 1.0

```python
l1_ratio = 1.0
```

**Verification:**
```python
assert_almost_equal(np.abs(a - b).max(), 0.0, decimal=decimal)
```

### Step 2: Assign shape = value

```python
shape = [size] * ndim
```

### Step 3: Assign z = rng.standard_normal(...)

```python
z = rng.standard_normal(shape)
```

### Step 4: Assign a = unknown.ravel(...)

```python
a = prox_tvl1(z.copy(), weight=weight, l1_ratio=l1_ratio, dgap_tol=dgap_tol, max_iter=10)[0][-1].ravel()
```

### Step 5: Assign b = unknown.ravel(...)

```python
b = prox_l1(z.copy(), weight)[-1].ravel()
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(np.abs(a - b).max(), 0.0, decimal=decimal)
```


## Complete Example

```python
# Setup
# Fixtures: rng, ndim, weight, size, decimal, dgap_tol

# Workflow
l1_ratio = 1.0
shape = [size] * ndim
z = rng.standard_normal(shape)
a = prox_tvl1(z.copy(), weight=weight, l1_ratio=l1_ratio, dgap_tol=dgap_tol, max_iter=10)[0][-1].ravel()
b = prox_l1(z.copy(), weight)[-1].ravel()
assert_almost_equal(np.abs(a - b).max(), 0.0, decimal=decimal)
```

## Next Steps


---

*Source: test_operators.py:26 | Complexity: Intermediate | Last updated: 2026-05-18*