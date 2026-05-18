# How To: Initvals Without Jitter

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test initvals without jitter

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `re`
- `warnings`
- `collections.abc`
- `typing`
- `unittest`
- `jax`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc.exceptions`
- `pymc.sampling.jax`

**Setup Required:**
```python
# Fixtures: sampler
```

## Step-by-Step Guide

### Step 1: Assign pytensor.config.on_opt_error = 'raise'

```python
pytensor.config.on_opt_error = 'raise'
```

**Verification:**
```python
assert np.allclose(trace1.posterior['a'].values[0], -3)
```

### Step 2: Call np.random.seed()

```python
np.random.seed(13244)
```

**Verification:**
```python
assert not np.allclose(trace2.posterior['a'].values[0], -3)
```

### Step 3: Assign obs = np.random.normal(...)

```python
obs = np.random.normal(10, 2, size=100)
```

### Step 4: Assign obs_at = pytensor.shared(...)

```python
obs_at = pytensor.shared(obs, borrow=True, name='obs')
```

### Step 5: Assign initvals = value

```python
initvals = {'a': -3}
```

**Verification:**
```python
assert np.allclose(trace1.posterior['a'].values[0], -3)
```

### Step 6: Assign a = pm.Uniform(...)

```python
a = pm.Uniform('a', -20, 20)
```

### Step 7: Assign b = pm.Deterministic(...)

```python
b = pm.Deterministic('b', a / 2.0)
```

### Step 8: Assign c = pm.Normal(...)

```python
c = pm.Normal('c', a, sigma=1.0, observed=obs_at)
```

### Step 9: Assign trace1 = sampler(...)

```python
trace1 = sampler(chains=1, tune=1, draws=1, random_seed=1322, initvals=initvals, jitter=False, keep_untransformed=True)
```

### Step 10: Assign trace2 = sampler(...)

```python
trace2 = sampler(chains=1, tune=1, draws=1, random_seed=1322, initvals=initvals, keep_untransformed=True)
```


## Complete Example

```python
# Setup
# Fixtures: sampler

# Workflow
pytensor.config.on_opt_error = 'raise'
np.random.seed(13244)
obs = np.random.normal(10, 2, size=100)
obs_at = pytensor.shared(obs, borrow=True, name='obs')
initvals = {'a': -3}
with pm.Model() as model:
    a = pm.Uniform('a', -20, 20)
    b = pm.Deterministic('b', a / 2.0)
    c = pm.Normal('c', a, sigma=1.0, observed=obs_at)
    trace1 = sampler(chains=1, tune=1, draws=1, random_seed=1322, initvals=initvals, jitter=False, keep_untransformed=True)
    trace2 = sampler(chains=1, tune=1, draws=1, random_seed=1322, initvals=initvals, keep_untransformed=True)
assert np.allclose(trace1.posterior['a'].values[0], -3)
assert not np.allclose(trace2.posterior['a'].values[0], -3)
```

## Next Steps


---

*Source: test_jax.py:139 | Complexity: Advanced | Last updated: 2026-05-18*