# How To: Components Expanded By Weights

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that components are expanded when size or weights are larger than components

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
# Fixtures: comp_dists
```

## Step-by-Step Guide

### Step 1: 'Test that components are expanded when size or weights are larger than components'

```python
'Test that components are expanded when size or weights are larger than components'
```

**Verification:**
```python
assert draws.shape == (3,) if univariate else (3, 3)
```

### Step 2: Assign mix = Mixture.dist(...)

```python
mix = Mixture.dist(w=Dirichlet.dist([1, 1], shape=(3, 2)), comp_dists=comp_dists, size=(3,))
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
assert draws.shape == (4, 3) if univariate else (4, 3, 3)
```

### Step 4: Assign mix = Mixture.dist(...)

```python
mix = Mixture.dist(w=Dirichlet.dist([1, 1], shape=(4, 3, 2)), comp_dists=comp_dists, size=(3,))
```

**Verification:**
```python
assert np.unique(draws).size == draws.size
```

### Step 5: Assign draws = mix.eval(...)

```python
draws = mix.eval()
```

**Verification:**
```python
assert draws.shape == (4, 3) if univariate else (4, 3, 3)
```

### Step 6: Assign univariate = value

```python
univariate = comp_dists[0].owner.op.ndim_supp == 0
```

### Step 7: Assign univariate = value

```python
univariate = comp_dists.owner.op.ndim_supp == 0
```


## Complete Example

```python
# Setup
# Fixtures: comp_dists

# Workflow
'Test that components are expanded when size or weights are larger than components'
if isinstance(comp_dists, list):
    univariate = comp_dists[0].owner.op.ndim_supp == 0
else:
    univariate = comp_dists.owner.op.ndim_supp == 0
mix = Mixture.dist(w=Dirichlet.dist([1, 1], shape=(3, 2)), comp_dists=comp_dists, size=(3,))
draws = mix.eval()
assert draws.shape == (3,) if univariate else (3, 3)
assert np.unique(draws).size == draws.size
mix = Mixture.dist(w=Dirichlet.dist([1, 1], shape=(4, 3, 2)), comp_dists=comp_dists, size=(3,))
draws = mix.eval()
assert draws.shape == (4, 3) if univariate else (4, 3, 3)
assert np.unique(draws).size == draws.size
```

## Next Steps


---

*Source: test_mixture.py:369 | Complexity: Intermediate | Last updated: 2026-05-18*