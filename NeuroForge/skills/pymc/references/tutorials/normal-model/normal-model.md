# How To: Normal Model

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test normal model

## Prerequisites

**Required Modules:**
- `logging`
- `warnings`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pytensor.compile.ops`
- `xarray`
- `pymc`
- `pymc.backends.base`
- `pymc.distributions.transforms`
- `pymc.pytensorf`
- `pymc.smc.kernels`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign data = st.norm.rvs(...)

```python
data = st.norm(10, 0.5).rvs(1000, random_state=np.random.RandomState(20160911))
```

**Verification:**
```python
assert_random_state_equal(initial_rng_state, np.random.get_state())
```

### Step 2: Assign initial_rng_state = np.random.get_state(...)

```python
initial_rng_state = np.random.get_state()
```

**Verification:**
```python
assert np.abs(post['mu'].mean() - 10) < 0.1
```

### Step 3: Call assert_random_state_equal()

```python
assert_random_state_equal(initial_rng_state, np.random.get_state())
```

**Verification:**
```python
assert np.abs(post['sigma'].mean() - 0.5) < 0.05
```

### Step 4: Assign post = idata.posterior.to_dataset.stack(...)

```python
post = idata.posterior.to_dataset().stack(sample=('chain', 'draw'))
```

**Verification:**
```python
assert np.abs(post['mu'].mean() - 10) < 0.1
```

### Step 5: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', 0, 3)
```

### Step 6: Assign sigma = pm.HalfNormal(...)

```python
sigma = pm.HalfNormal('sigma', 1)
```

### Step 7: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', mu, sigma, observed=data)
```

### Step 8: Assign idata = pm.sample_smc(...)

```python
idata = pm.sample_smc(draws=2000, kernel=pm.smc.MH)
```


## Complete Example

```python
# Workflow
data = st.norm(10, 0.5).rvs(1000, random_state=np.random.RandomState(20160911))
initial_rng_state = np.random.get_state()
with pm.Model() as m:
    mu = pm.Normal('mu', 0, 3)
    sigma = pm.HalfNormal('sigma', 1)
    y = pm.Normal('y', mu, sigma, observed=data)
    idata = pm.sample_smc(draws=2000, kernel=pm.smc.MH)
assert_random_state_equal(initial_rng_state, np.random.get_state())
post = idata.posterior.to_dataset().stack(sample=('chain', 'draw'))
assert np.abs(post['mu'].mean() - 10) < 0.1
assert np.abs(post['sigma'].mean() - 0.5) < 0.05
```

## Next Steps


---

*Source: test_smc.py:275 | Complexity: Advanced | Last updated: 2026-05-18*