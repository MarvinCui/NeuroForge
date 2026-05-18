# How To: Transform Samples

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test transform samples

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
# Fixtures: sampler, postprocessing_backend, chains, postprocessing_vectorize
```

## Step-by-Step Guide

### Step 1: Assign pytensor.config.on_opt_error = 'raise'

```python
pytensor.config.on_opt_error = 'raise'
```

**Verification:**
```python
assert np.allclose(np.exp(log_vals), trans_vals)
```

### Step 2: Call np.random.seed()

```python
np.random.seed(13244)
```

**Verification:**
```python
assert 8 < trace.posterior['a'].mean() < 11
```

### Step 3: Assign obs = np.random.normal(...)

```python
obs = np.random.normal(10, 2, size=100)
```

**Verification:**
```python
assert 1.5 < trace.posterior['sigma'].mean() < 2.5
```

### Step 4: Assign obs_at = pytensor.shared(...)

```python
obs_at = pytensor.shared(obs, borrow=True, name='obs')
```

**Verification:**
```python
assert -11 < trace.posterior['a'].mean() < -8
```

### Step 5: Assign log_vals = value

```python
log_vals = trace.posterior['sigma_log__'].values
```

**Verification:**
```python
assert 1.5 < trace.posterior['sigma'].mean() < 2.5
```

### Step 6: Assign trans_vals = value

```python
trans_vals = trace.posterior['sigma'].values
```

**Verification:**
```python
assert np.allclose(np.exp(log_vals), trans_vals)
```

### Step 7: Call obs_at.set_value()

```python
obs_at.set_value(-obs)
```

**Verification:**
```python
assert -11 < trace.posterior['a'].mean() < -8
```

### Step 8: Assign a = pm.Uniform(...)

```python
a = pm.Uniform('a', -20, 20)
```

### Step 9: Assign sigma = pm.HalfNormal(...)

```python
sigma = pm.HalfNormal('sigma', shape=(2,))
```

### Step 10: Assign b = pm.Normal(...)

```python
b = pm.Normal('b', a, sigma=sigma.mean(), observed=obs_at)
```

### Step 11: Assign trace = sampler(...)

```python
trace = sampler(chains=chains, random_seed=1322, keep_untransformed=True, postprocessing_backend=postprocessing_backend, postprocessing_vectorize=postprocessing_vectorize)
```

### Step 12: Assign trace = sampler(...)

```python
trace = sampler(chains=chains, random_seed=1322, keep_untransformed=False, postprocessing_backend=postprocessing_backend)
```


## Complete Example

```python
# Setup
# Fixtures: sampler, postprocessing_backend, chains, postprocessing_vectorize

# Workflow
pytensor.config.on_opt_error = 'raise'
np.random.seed(13244)
obs = np.random.normal(10, 2, size=100)
obs_at = pytensor.shared(obs, borrow=True, name='obs')
with pm.Model() as model:
    a = pm.Uniform('a', -20, 20)
    sigma = pm.HalfNormal('sigma', shape=(2,))
    b = pm.Normal('b', a, sigma=sigma.mean(), observed=obs_at)
    trace = sampler(chains=chains, random_seed=1322, keep_untransformed=True, postprocessing_backend=postprocessing_backend, postprocessing_vectorize=postprocessing_vectorize)
log_vals = trace.posterior['sigma_log__'].values
trans_vals = trace.posterior['sigma'].values
assert np.allclose(np.exp(log_vals), trans_vals)
assert 8 < trace.posterior['a'].mean() < 11
assert 1.5 < trace.posterior['sigma'].mean() < 2.5
obs_at.set_value(-obs)
with model:
    trace = sampler(chains=chains, random_seed=1322, keep_untransformed=False, postprocessing_backend=postprocessing_backend)
assert -11 < trace.posterior['a'].mean() < -8
assert 1.5 < trace.posterior['sigma'].mean() < 2.5
```

## Next Steps


---

*Source: test_jax.py:67 | Complexity: Advanced | Last updated: 2026-05-18*