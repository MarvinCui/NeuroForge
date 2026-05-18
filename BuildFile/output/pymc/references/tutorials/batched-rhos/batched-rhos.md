# How To: Batched Rhos

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test batched rhos

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc`
- `pymc.distributions.continuous`
- `pymc.distributions.distribution`
- `pymc.distributions.multivariate`
- `pymc.distributions.shape_utils`
- `pymc.distributions.timeseries`
- `pymc.logprob.basic`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.sampling.mcmc`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
ar_order, steps, batch_size = (3, 100, 5)
```

**Verification:**
```python
assert y_eval.shape == (batch_size, steps)
```

### Step 2: Assign beta_tp = np.random.randn(...)

```python
beta_tp = np.random.randn(batch_size, ar_order)
```

**Verification:**
```python
assert np.all(abs(y_eval[1]) < 5)
```

### Step 3: Assign y_tp = np.random.randn(...)

```python
y_tp = np.random.randn(batch_size, steps)
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(t0.compile_logp()(t0.initial_point()), t1.compile_logp()(t1.initial_point()))
```

### Step 5: Assign unknown = 0

```python
beta_tp[1] = 0
```

### Step 6: Assign y_eval = unknown.eval(...)

```python
y_eval = t0['y'].eval({t0['beta']: beta_tp})
```

**Verification:**
```python
assert y_eval.shape == (batch_size, steps)
```

### Step 7: Assign beta = Normal(...)

```python
beta = Normal('beta', 0.0, 1.0, shape=(batch_size, ar_order), initval=beta_tp)
```

### Step 8: Call AR()

```python
AR('y', beta, sigma=1.0, init_dist=Normal.dist(0, 1), shape=(batch_size, steps), initval=y_tp)
```

### Step 9: Assign beta = Normal(...)

```python
beta = Normal('beta', 0.0, 1.0, shape=(batch_size, ar_order), initval=beta_tp)
```

### Step 10: Call AR()

```python
AR(f'y_{i}', beta[i], init_dist=Normal.dist(0, 1), sigma=1.0, shape=steps, initval=y_tp[i])
```


## Complete Example

```python
# Workflow
ar_order, steps, batch_size = (3, 100, 5)
beta_tp = np.random.randn(batch_size, ar_order)
y_tp = np.random.randn(batch_size, steps)
with Model() as t0:
    beta = Normal('beta', 0.0, 1.0, shape=(batch_size, ar_order), initval=beta_tp)
    AR('y', beta, sigma=1.0, init_dist=Normal.dist(0, 1), shape=(batch_size, steps), initval=y_tp)
with Model() as t1:
    beta = Normal('beta', 0.0, 1.0, shape=(batch_size, ar_order), initval=beta_tp)
    for i in range(batch_size):
        AR(f'y_{i}', beta[i], init_dist=Normal.dist(0, 1), sigma=1.0, shape=steps, initval=y_tp[i])
np.testing.assert_allclose(t0.compile_logp()(t0.initial_point()), t1.compile_logp()(t1.initial_point()))
beta_tp[1] = 0
y_eval = t0['y'].eval({t0['beta']: beta_tp})
assert y_eval.shape == (batch_size, steps)
assert np.all(abs(y_eval[1]) < 5)
```

## Next Steps


---

*Source: test_timeseries.py:543 | Complexity: Advanced | Last updated: 2026-05-18*