# How To: Sample

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `os`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.data`
- `pymc.pytensorf`

**Setup Required:**
```python
# Fixtures: seeded_test
```

## Step-by-Step Guide

### Step 1: Assign x = np.random.normal(...)

```python
x = np.random.normal(size=100)
```

**Verification:**
```python
assert prior_trace0.prior['b'].shape == (1, 1000)
```

### Step 2: Assign y = value

```python
y = x + np.random.normal(scale=0.01, size=100)
```

**Verification:**
```python
assert prior_trace0.prior_predictive['obs'].shape == (1, 1000, 100)
```

### Step 3: Assign x_pred = np.linspace(...)

```python
x_pred = np.linspace(-3, 3, 200, dtype='float32')
```

**Verification:**
```python
assert prior_trace1.prior_predictive['obs'].shape == (1, 1000, 200)
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x, pp_trace0.posterior_predictive['obs'].mean(('chain', 'draw')), atol=0.1)
```

**Verification:**
```python
assert pp_trace0.posterior_predictive['obs'].shape == (1, 1000, 100)
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x_pred, pp_trace1.posterior_predictive['obs'].mean(('chain', 'draw')), atol=0.1)
```

**Verification:**
```python
assert pp_trace1.posterior_predictive['obs'].shape == (1, 1000, 200)
```

### Step 6: Assign x_shared = pm.Data(...)

```python
x_shared = pm.Data('x_shared', x)
```

### Step 7: Assign b = pm.Normal(...)

```python
b = pm.Normal('b', 0.0, 10.0)
```

### Step 8: Call pm.Normal()

```python
pm.Normal('obs', b * x_shared, np.sqrt(0.01), observed=y, shape=x_shared.shape)
```

### Step 9: Assign prior_trace0 = pm.sample_prior_predictive(...)

```python
prior_trace0 = pm.sample_prior_predictive(1000)
```

### Step 10: Assign idata = pm.sample(...)

```python
idata = pm.sample(1000, tune=1000, chains=1)
```

### Step 11: Assign pp_trace0 = pm.sample_posterior_predictive(...)

```python
pp_trace0 = pm.sample_posterior_predictive(idata)
```

### Step 12: Call x_shared.set_value()

```python
x_shared.set_value(x_pred)
```

### Step 13: Assign prior_trace1 = pm.sample_prior_predictive(...)

```python
prior_trace1 = pm.sample_prior_predictive(1000)
```

### Step 14: Assign pp_trace1 = pm.sample_posterior_predictive(...)

```python
pp_trace1 = pm.sample_posterior_predictive(idata)
```


## Complete Example

```python
# Setup
# Fixtures: seeded_test

# Workflow
x = np.random.normal(size=100)
y = x + np.random.normal(scale=0.01, size=100)
x_pred = np.linspace(-3, 3, 200, dtype='float32')
with pm.Model():
    x_shared = pm.Data('x_shared', x)
    b = pm.Normal('b', 0.0, 10.0)
    pm.Normal('obs', b * x_shared, np.sqrt(0.01), observed=y, shape=x_shared.shape)
    prior_trace0 = pm.sample_prior_predictive(1000)
    idata = pm.sample(1000, tune=1000, chains=1)
    pp_trace0 = pm.sample_posterior_predictive(idata)
    x_shared.set_value(x_pred)
    prior_trace1 = pm.sample_prior_predictive(1000)
    pp_trace1 = pm.sample_posterior_predictive(idata)
assert prior_trace0.prior['b'].shape == (1, 1000)
assert prior_trace0.prior_predictive['obs'].shape == (1, 1000, 100)
assert prior_trace1.prior_predictive['obs'].shape == (1, 1000, 200)
assert pp_trace0.posterior_predictive['obs'].shape == (1, 1000, 100)
np.testing.assert_allclose(x, pp_trace0.posterior_predictive['obs'].mean(('chain', 'draw')), atol=0.1)
assert pp_trace1.posterior_predictive['obs'].shape == (1, 1000, 200)
np.testing.assert_allclose(x_pred, pp_trace1.posterior_predictive['obs'].mean(('chain', 'draw')), atol=0.1)
```

## Next Steps


---

*Source: test_data.py:41 | Complexity: Advanced | Last updated: 2026-05-18*