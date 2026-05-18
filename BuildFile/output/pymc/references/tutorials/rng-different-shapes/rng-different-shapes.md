# How To: Rng Different Shapes

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rng different shapes

## Prerequisites

**Required Modules:**
- `functools`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `scipy.stats`
- `pytensor.compile.mode`
- `pymc`
- `pymc.distributions.continuous`
- `pymc.distributions.dist_math`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.testing`
- `polyagamma`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(123)
```

**Verification:**
```python
assert len(np.unique(draws)) == draws.size
```

### Step 2: Assign alpha = np.abs(...)

```python
alpha = np.abs(rng.normal(size=5))
```

### Step 3: Assign beta = np.abs(...)

```python
beta = np.abs(rng.normal(size=(3, 1)))
```

### Step 4: Assign draws = pm.draw(...)

```python
draws = pm.draw(pm.Weibull.dist(alpha, beta), random_seed=rng)
```

**Verification:**
```python
assert len(np.unique(draws)) == draws.size
```


## Complete Example

```python
# Workflow
rng = np.random.default_rng(123)
alpha = np.abs(rng.normal(size=5))
beta = np.abs(rng.normal(size=(3, 1)))
draws = pm.draw(pm.Weibull.dist(alpha, beta), random_seed=rng)
assert len(np.unique(draws)) == draws.size
```

## Next Steps


---

*Source: test_continuous.py:2464 | Complexity: Intermediate | Last updated: 2026-05-18*