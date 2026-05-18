# How To: Component Choice Random

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that mixture choices change over evaluations

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test that mixture choices change over evaluations'

```python
'Test that mixture choices change over evaluations'
```

**Verification:**
```python
assert np.unique(draws > 0).size == 2
```

### Step 2: Assign draws = draw(...)

```python
draws = draw(mix, draws=20, random_seed=self.get_random_state())
```

**Verification:**
```python
assert np.unique(draws > 0).size == 2
```

### Step 3: Assign weights = value

```python
weights = [0.5, 0.5]
```

### Step 4: Assign components = value

```python
components = [Normal.dist(-10, 0.01), Normal.dist(10, 0.01)]
```

### Step 5: Assign mix = Mixture.dist(...)

```python
mix = Mixture.dist(weights, components)
```


## Complete Example

```python
# Workflow
'Test that mixture choices change over evaluations'
with Model() as m:
    weights = [0.5, 0.5]
    components = [Normal.dist(-10, 0.01), Normal.dist(10, 0.01)]
    mix = Mixture.dist(weights, components)
draws = draw(mix, draws=20, random_seed=self.get_random_state())
assert np.unique(draws > 0).size == 2
```

## Next Steps


---

*Source: test_mixture.py:347 | Complexity: Intermediate | Last updated: 2026-05-18*