# How To: Change Dist Size

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test change dist size

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytensor.tensor.random.op`
- `scipy.special`
- `pymc.distributions`
- `pymc.distributions.mixture`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.math`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.sampling.mcmc`
- `pymc.step_methods`
- `pymc.testing`
- `pymc.vartypes`

**Setup Required:**
```python
# Fixtures: comp_dists, expand
```

## Step-by-Step Guide

### Step 1: Assign mix = Mixture.dist(...)

```python
mix = Mixture.dist(w=Dirichlet.dist([1, 1]), comp_dists=comp_dists)
```

**Verification:**
```python
assert draws.shape == expected_shape
```

### Step 2: Assign mix = change_dist_size(...)

```python
mix = change_dist_size(mix, new_size=(4,), expand=expand)
```

**Verification:**
```python
assert np.unique(draws).size == draws.size
```

### Step 3: Assign draws = mix.eval(...)

```python
draws = mix.eval()
```

**Verification:**
```python
assert draws.shape == expected_shape
```

### Step 4: Assign expected_shape = value

```python
expected_shape = (4,) if univariate else (4, 3)
```

**Verification:**
```python
assert np.unique(draws).size == draws.size
```

### Step 5: Assign mix = Mixture.dist(...)

```python
mix = Mixture.dist(w=Dirichlet.dist([1, 1]), comp_dists=comp_dists, size=(3,))
```

### Step 6: Assign mix = change_dist_size(...)

```python
mix = change_dist_size(mix, new_size=(5, 4), expand=expand)
```

### Step 7: Assign draws = mix.eval(...)

```python
draws = mix.eval()
```

### Step 8: Assign expected_shape = value

```python
expected_shape = (5, 4) if univariate else (5, 4, 3)
```

**Verification:**
```python
assert draws.shape == expected_shape
```

### Step 9: Assign univariate = value

```python
univariate = comp_dists[0].owner.op.ndim_supp == 0
```

### Step 10: Assign univariate = value

```python
univariate = comp_dists.owner.op.ndim_supp == 0
```

### Step 11: Assign expected_shape = value

```python
expected_shape = (*expected_shape, 3)
```


## Complete Example

```python
# Setup
# Fixtures: comp_dists, expand

# Workflow
if isinstance(comp_dists, list):
    univariate = comp_dists[0].owner.op.ndim_supp == 0
else:
    univariate = comp_dists.owner.op.ndim_supp == 0
mix = Mixture.dist(w=Dirichlet.dist([1, 1]), comp_dists=comp_dists)
mix = change_dist_size(mix, new_size=(4,), expand=expand)
draws = mix.eval()
expected_shape = (4,) if univariate else (4, 3)
assert draws.shape == expected_shape
assert np.unique(draws).size == draws.size
mix = Mixture.dist(w=Dirichlet.dist([1, 1]), comp_dists=comp_dists, size=(3,))
mix = change_dist_size(mix, new_size=(5, 4), expand=expand)
draws = mix.eval()
expected_shape = (5, 4) if univariate else (5, 4, 3)
if expand:
    expected_shape = (*expected_shape, 3)
assert draws.shape == expected_shape
assert np.unique(draws).size == draws.size
```

## Next Steps


---

*Source: test_mixture.py:407 | Complexity: Advanced | Last updated: 2026-05-18*