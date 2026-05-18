# How To: Elbo

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test elbo

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pymc`
- `pymc.pytensorf`
- `pymc.variational.approximations`
- `pymc.variational.operators`
- `tests`


## Step-by-Step Guide

### Step 1: Assign mu0 = 1.5

```python
mu0 = 1.5
```

### Step 2: Assign sigma = 1.0

```python
sigma = 1.0
```

### Step 3: Assign y_obs = np.array(...)

```python
y_obs = np.array([1.6, 1.4])
```

### Step 4: Assign post_mu = np.array(...)

```python
post_mu = np.array([1.88], dtype=pytensor.config.floatX)
```

### Step 5: Assign post_sigma = np.array(...)

```python
post_sigma = np.array([1], dtype=pytensor.config.floatX)
```

### Step 6: Assign mean_field = MeanField(...)

```python
mean_field = MeanField(model=model)
```

### Step 7: Assign elbo = value

```python
elbo = -KL(mean_field)()(10000)
```

### Step 8: Call unknown.set_value()

```python
mean_field.shared_params['mu'].set_value(post_mu)
```

### Step 9: Call unknown.set_value()

```python
mean_field.shared_params['rho'].set_value(np.log(np.exp(post_sigma) - 1))
```

### Step 10: Assign f = pytensor.function(...)

```python
f = pytensor.function([], elbo)
```

### Step 11: Assign elbo_mc = f(...)

```python
elbo_mc = f()
```

### Step 12: Assign elbo_true = value

```python
elbo_true = -0.5 * (3 + 3 * post_mu ** 2 - 2 * (y_obs[0] + y_obs[1] + mu0) * post_mu + y_obs[0] ** 2 + y_obs[1] ** 2 + mu0 ** 2 + 3 * np.log(2 * np.pi)) + 0.5 * (np.log(2 * np.pi) + 1)
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(elbo_mc, elbo_true, rtol=0, atol=0.1)
```

### Step 14: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', mu=mu0, sigma=sigma)
```

### Step 15: Call pm.Normal()

```python
pm.Normal('y', mu=mu, sigma=1, observed=y_obs)
```


## Complete Example

```python
# Workflow
mu0 = 1.5
sigma = 1.0
y_obs = np.array([1.6, 1.4])
post_mu = np.array([1.88], dtype=pytensor.config.floatX)
post_sigma = np.array([1], dtype=pytensor.config.floatX)
with pm.Model() as model:
    mu = pm.Normal('mu', mu=mu0, sigma=sigma)
    pm.Normal('y', mu=mu, sigma=1, observed=y_obs)
mean_field = MeanField(model=model)
elbo = -KL(mean_field)()(10000)
mean_field.shared_params['mu'].set_value(post_mu)
mean_field.shared_params['rho'].set_value(np.log(np.exp(post_sigma) - 1))
f = pytensor.function([], elbo)
elbo_mc = f()
elbo_true = -0.5 * (3 + 3 * post_mu ** 2 - 2 * (y_obs[0] + y_obs[1] + mu0) * post_mu + y_obs[0] ** 2 + y_obs[1] ** 2 + mu0 ** 2 + 3 * np.log(2 * np.pi)) + 0.5 * (np.log(2 * np.pi) + 1)
np.testing.assert_allclose(elbo_mc, elbo_true, rtol=0, atol=0.1)
```

## Next Steps


---

*Source: test_approximations.py:46 | Complexity: Advanced | Last updated: 2026-05-18*