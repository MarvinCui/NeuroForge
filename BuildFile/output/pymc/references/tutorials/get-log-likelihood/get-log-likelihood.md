# How To: Get Log Likelihood

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test get log likelihood

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign obs = np.random.normal(...)

```python
obs = np.random.normal(10, 2, size=100)
```

**Verification:**
```python
assert np.allclose(b_jax.reshape(-1), b_true.reshape(-1))
```

### Step 2: Assign obs_at = pytensor.shared(...)

```python
obs_at = pytensor.shared(obs, borrow=True, name='obs')
```

### Step 3: Assign b_true = value

```python
b_true = trace.log_likelihood.b.values
```

### Step 4: Assign a = np.array(...)

```python
a = np.array(trace.posterior.a)
```

### Step 5: Assign sigma_log_ = np.log(...)

```python
sigma_log_ = np.log(np.array(trace.posterior.sigma))
```

### Step 6: Assign b_jax = value

```python
b_jax = _get_log_likelihood(model, [a, sigma_log_])['b']
```

**Verification:**
```python
assert np.allclose(b_jax.reshape(-1), b_true.reshape(-1))
```

### Step 7: Assign a = pm.Normal(...)

```python
a = pm.Normal('a', 0, 2)
```

### Step 8: Assign sigma = pm.HalfNormal(...)

```python
sigma = pm.HalfNormal('sigma')
```

### Step 9: Assign b = pm.Normal(...)

```python
b = pm.Normal('b', a, sigma=sigma, observed=obs_at)
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
```

### Step 11: Assign trace = pm.sample(...)

```python
trace = pm.sample(tune=10, draws=10, chains=2, random_seed=1322, idata_kwargs={'log_likelihood': True})
```


## Complete Example

```python
# Workflow
obs = np.random.normal(10, 2, size=100)
obs_at = pytensor.shared(obs, borrow=True, name='obs')
with pm.Model() as model:
    a = pm.Normal('a', 0, 2)
    sigma = pm.HalfNormal('sigma')
    b = pm.Normal('b', a, sigma=sigma, observed=obs_at)
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
        trace = pm.sample(tune=10, draws=10, chains=2, random_seed=1322, idata_kwargs={'log_likelihood': True})
b_true = trace.log_likelihood.b.values
a = np.array(trace.posterior.a)
sigma_log_ = np.log(np.array(trace.posterior.sigma))
b_jax = _get_log_likelihood(model, [a, sigma_log_])['b']
assert np.allclose(b_jax.reshape(-1), b_true.reshape(-1))
```

## Next Steps


---

*Source: test_jax.py:184 | Complexity: Advanced | Last updated: 2026-05-18*