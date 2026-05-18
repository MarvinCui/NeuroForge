# How To: Scale Cost To Minibatch Works

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test scale cost to minibatch works

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pymc`
- `pymc.pytensorf`
- `pymc.variational.approximations`
- `pymc.variational.operators`
- `tests`

**Setup Required:**
```python
# Fixtures: aux_total_size
```

## Step-by-Step Guide

### Step 1: Assign mu0 = 1.5

```python
mu0 = 1.5
```

**Verification:**
```python
assert pytensor.config.floatX == 'float64'
```

### Step 2: Assign sigma = 1.0

```python
sigma = 1.0
```

**Verification:**
```python
assert pytensor.config.warn_float64 == 'ignore'
```

### Step 3: Assign y_obs = np.array(...)

```python
y_obs = np.array([1.6, 1.4])
```

**Verification:**
```python
assert mean_field_1.scale_cost_to_minibatch
```

### Step 4: Assign beta = value

```python
beta = len(y_obs) / float(aux_total_size)
```

**Verification:**
```python
assert mean_field_1.scale_cost_to_minibatch
```

### Step 5: Assign post_mu = np.array(...)

```python
post_mu = np.array([1.88], dtype=pytensor.config.floatX)
```

**Verification:**
```python
assert not mean_field_2.scale_cost_to_minibatch
```

### Step 6: Assign post_sigma = np.array(...)

```python
post_sigma = np.array([1], dtype=pytensor.config.floatX)
```

### Step 7: Assign elbo_via_total_size_unscaled = value

```python
elbo_via_total_size_unscaled = -KL(mean_field_2)()(10000)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(elbo_via_total_size_unscaled.eval(), elbo_via_total_size_scaled.eval() * floatX(1 / beta), rtol=0.02, atol=0.1)
```

### Step 9: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', mu=mu0, sigma=sigma)
```

### Step 10: Call pm.Normal()

```python
pm.Normal('y', mu=mu, sigma=1, observed=y_obs, total_size=aux_total_size)
```

### Step 11: Assign mean_field_1 = MeanField(...)

```python
mean_field_1 = MeanField()
```

**Verification:**
```python
assert mean_field_1.scale_cost_to_minibatch
```

### Step 12: Call unknown.set_value()

```python
mean_field_1.shared_params['mu'].set_value(post_mu)
```

### Step 13: Call unknown.set_value()

```python
mean_field_1.shared_params['rho'].set_value(np.log(np.exp(post_sigma) - 1))
```

### Step 14: Assign elbo_via_total_size_scaled = value

```python
elbo_via_total_size_scaled = -KL(mean_field_1)()(10000)
```

### Step 15: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', mu=mu0, sigma=sigma)
```

### Step 16: Call pm.Normal()

```python
pm.Normal('y', mu=mu, sigma=1, observed=y_obs, total_size=aux_total_size)
```

### Step 17: Assign mean_field_2 = MeanField(...)

```python
mean_field_2 = MeanField()
```

**Verification:**
```python
assert mean_field_1.scale_cost_to_minibatch
```

### Step 18: Assign mean_field_2.scale_cost_to_minibatch = False

```python
mean_field_2.scale_cost_to_minibatch = False
```

**Verification:**
```python
assert not mean_field_2.scale_cost_to_minibatch
```

### Step 19: Call unknown.set_value()

```python
mean_field_2.shared_params['mu'].set_value(post_mu)
```

### Step 20: Call unknown.set_value()

```python
mean_field_2.shared_params['rho'].set_value(np.log(np.exp(post_sigma) - 1))
```


## Complete Example

```python
# Setup
# Fixtures: aux_total_size

# Workflow
mu0 = 1.5
sigma = 1.0
y_obs = np.array([1.6, 1.4])
beta = len(y_obs) / float(aux_total_size)
with pytensor.config.change_flags(floatX='float64', warn_float64='ignore'):
    assert pytensor.config.floatX == 'float64'
    assert pytensor.config.warn_float64 == 'ignore'
    post_mu = np.array([1.88], dtype=pytensor.config.floatX)
    post_sigma = np.array([1], dtype=pytensor.config.floatX)
    with pm.Model():
        mu = pm.Normal('mu', mu=mu0, sigma=sigma)
        pm.Normal('y', mu=mu, sigma=1, observed=y_obs, total_size=aux_total_size)
        mean_field_1 = MeanField()
        assert mean_field_1.scale_cost_to_minibatch
        mean_field_1.shared_params['mu'].set_value(post_mu)
        mean_field_1.shared_params['rho'].set_value(np.log(np.exp(post_sigma) - 1))
        elbo_via_total_size_scaled = -KL(mean_field_1)()(10000)
    with pm.Model():
        mu = pm.Normal('mu', mu=mu0, sigma=sigma)
        pm.Normal('y', mu=mu, sigma=1, observed=y_obs, total_size=aux_total_size)
        mean_field_2 = MeanField()
        assert mean_field_1.scale_cost_to_minibatch
        mean_field_2.scale_cost_to_minibatch = False
        assert not mean_field_2.scale_cost_to_minibatch
        mean_field_2.shared_params['mu'].set_value(post_mu)
        mean_field_2.shared_params['rho'].set_value(np.log(np.exp(post_sigma) - 1))
    elbo_via_total_size_unscaled = -KL(mean_field_2)()(10000)
    np.testing.assert_allclose(elbo_via_total_size_unscaled.eval(), elbo_via_total_size_scaled.eval() * floatX(1 / beta), rtol=0.02, atol=0.1)
```

## Next Steps


---

*Source: test_approximations.py:82 | Complexity: Advanced | Last updated: 2026-05-18*