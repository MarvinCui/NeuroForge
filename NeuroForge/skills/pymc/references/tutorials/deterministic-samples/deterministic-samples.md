# How To: Deterministic Samples

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test deterministic samples

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
assert 8 < trace.posterior['a'].mean() < 11
```

### Step 2: Call np.random.seed()

```python
np.random.seed(13244)
```

**Verification:**
```python
assert np.allclose(trace.posterior['b'].values, trace.posterior['a'].values / 2)
```

### Step 3: Assign obs = np.random.normal(...)

```python
obs = np.random.normal(10, 2, size=100)
```

### Step 4: Assign obs_at = pytensor.shared(...)

```python
obs_at = pytensor.shared(obs, borrow=True, name='obs')
```

**Verification:**
```python
assert 8 < trace.posterior['a'].mean() < 11
```

### Step 5: Assign a = pm.Uniform(...)

```python
a = pm.Uniform('a', -20, 20)
```

### Step 6: Assign b = pm.Deterministic(...)

```python
b = pm.Deterministic('b', a / 2.0)
```

### Step 7: Assign c = pm.Normal(...)

```python
c = pm.Normal('c', a, sigma=1.0, observed=obs_at)
```

### Step 8: Assign trace = sampler(...)

```python
trace = sampler(chains=2, random_seed=1322, keep_untransformed=True)
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
with pm.Model() as model:
    a = pm.Uniform('a', -20, 20)
    b = pm.Deterministic('b', a / 2.0)
    c = pm.Normal('c', a, sigma=1.0, observed=obs_at)
    trace = sampler(chains=2, random_seed=1322, keep_untransformed=True)
assert 8 < trace.posterior['a'].mean() < 11
assert np.allclose(trace.posterior['b'].values, trace.posterior['a'].values / 2)
```

## Next Steps


---

*Source: test_jax.py:115 | Complexity: Advanced | Last updated: 2026-05-18*