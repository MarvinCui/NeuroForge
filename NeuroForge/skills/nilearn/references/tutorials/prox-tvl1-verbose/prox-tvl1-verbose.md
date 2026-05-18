# How To: Prox Tvl1 Verbose

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test prox tvl1 verbose

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
# Fixtures: rng, verbose
```

## Step-by-Step Guide

### Step 1: Assign l1_ratio = 1.0

```python
l1_ratio = 1.0
```

### Step 2: Assign size = 15

```python
size = 15
```

### Step 3: Assign dgap_tol = 1e-07

```python
dgap_tol = 1e-07
```

### Step 4: Assign ndim = 3

```python
ndim = 3
```

### Step 5: Assign weight = value

```python
weight = -10
```

### Step 6: Assign shape = value

```python
shape = [size] * ndim
```

### Step 7: Assign z = rng.standard_normal(...)

```python
z = rng.standard_normal(shape)
```

### Step 8: Call prox_tvl1()

```python
prox_tvl1(z.copy(), weight=weight, l1_ratio=l1_ratio, dgap_tol=dgap_tol, max_iter=10, val_min=-np.inf, val_max=np.inf, verbose=verbose, x_tol=1e-07)
```


## Complete Example

```python
# Setup
# Fixtures: rng, verbose

# Workflow
l1_ratio = 1.0
size = 15
dgap_tol = 1e-07
ndim = 3
weight = -10
shape = [size] * ndim
z = rng.standard_normal(shape)
prox_tvl1(z.copy(), weight=weight, l1_ratio=l1_ratio, dgap_tol=dgap_tol, max_iter=10, val_min=-np.inf, val_max=np.inf, verbose=verbose, x_tol=1e-07)
```

## Next Steps


---

*Source: test_operators.py:51 | Complexity: Advanced | Last updated: 2026-05-18*