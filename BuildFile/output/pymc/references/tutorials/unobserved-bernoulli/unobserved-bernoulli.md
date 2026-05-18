# How To: Unobserved Bernoulli

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test unobserved bernoulli

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

### Step 1: Assign n = 10

```python
n = 10
```

**Verification:**
```python
assert np.all(np.median(trace['z'], axis=0) == z_true)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(20160911)
```

### Step 3: Assign z_true = np.zeros(...)

```python
z_true = np.zeros(n, dtype=int)
```

### Step 4: Assign unknown = 1

```python
z_true[int(n / 2):] = 1
```

### Step 5: Assign y = st.norm.rvs(...)

```python
y = st.norm(np.array([-1, 1])[z_true], 0.25).rvs(random_state=rng)
```

**Verification:**
```python
assert np.all(np.median(trace['z'], axis=0) == z_true)
```

### Step 6: Assign z = pm.Bernoulli(...)

```python
z = pm.Bernoulli('z', p=0.5, size=n)
```

### Step 7: Assign mu = pm.math.switch(...)

```python
mu = pm.math.switch(z, 1.0, -1.0)
```

### Step 8: Assign like = pm.Normal(...)

```python
like = pm.Normal('like', mu=mu, sigma=0.25, observed=y)
```

### Step 9: Assign trace = pm.sample_smc(...)

```python
trace = pm.sample_smc(chains=1, return_inferencedata=False)
```


## Complete Example

```python
# Workflow
n = 10
rng = np.random.RandomState(20160911)
z_true = np.zeros(n, dtype=int)
z_true[int(n / 2):] = 1
y = st.norm(np.array([-1, 1])[z_true], 0.25).rvs(random_state=rng)
with pm.Model() as m:
    z = pm.Bernoulli('z', p=0.5, size=n)
    mu = pm.math.switch(z, 1.0, -1.0)
    like = pm.Normal('like', mu=mu, sigma=0.25, observed=y)
    trace = pm.sample_smc(chains=1, return_inferencedata=False)
assert np.all(np.median(trace['z'], axis=0) == z_true)
```

## Next Steps


---

*Source: test_smc.py:111 | Complexity: Advanced | Last updated: 2026-05-18*