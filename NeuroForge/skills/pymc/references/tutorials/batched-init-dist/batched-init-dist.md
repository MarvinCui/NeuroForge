# How To: Batched Init Dist

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test batched init dist

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
assert y_eval.shape == (batch_size, steps + ar_order)
```

### Step 2: Assign beta_tp = pytensor.shared(...)

```python
beta_tp = pytensor.shared(np.random.randn(ar_order), shape=(3,))
```

**Verification:**
```python
assert np.allclose(y_eval[:, -10:].mean(-1), np.arange(batch_size) * 100, rtol=0.1, atol=0.5)
```

### Step 3: Assign y_tp = np.random.randn(...)

```python
y_tp = np.random.randn(batch_size, steps)
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(t0.compile_logp()(t0.initial_point()), t1.compile_logp()(t1.initial_point()))
```

### Step 5: Call beta_tp.set_value()

```python
beta_tp.set_value(np.full((ar_order,), 1 / ar_order))
```

### Step 6: Assign init_dist = value

```python
init_dist = t0['y'].owner.inputs[2]
```

### Step 7: Assign init_dist_tp = np.full(...)

```python
init_dist_tp = np.full((batch_size, ar_order), (np.arange(batch_size) * 100)[:, None])
```

### Step 8: Assign y_eval = unknown.eval(...)

```python
y_eval = t0['y'].eval({init_dist: init_dist_tp})
```

**Verification:**
```python
assert y_eval.shape == (batch_size, steps + ar_order)
```

### Step 9: Assign init_dist = Normal.dist(...)

```python
init_dist = Normal.dist(0.0, 100.0, size=(batch_size, ar_order))
```

### Step 10: Call AR()

```python
AR('y', beta_tp, sigma=0.01, init_dist=init_dist, steps=steps, initval=y_tp)
```

### Step 11: Call AR()

```python
AR(f'y_{i}', beta_tp, sigma=0.01, shape=steps, initval=y_tp[i], init_dist=Normal.dist(0, 100, shape=steps))
```


## Complete Example

```python
# Workflow
ar_order, steps, batch_size = (3, 100, 5)
beta_tp = pytensor.shared(np.random.randn(ar_order), shape=(3,))
y_tp = np.random.randn(batch_size, steps)
with Model() as t0:
    init_dist = Normal.dist(0.0, 100.0, size=(batch_size, ar_order))
    AR('y', beta_tp, sigma=0.01, init_dist=init_dist, steps=steps, initval=y_tp)
with Model() as t1:
    for i in range(batch_size):
        AR(f'y_{i}', beta_tp, sigma=0.01, shape=steps, initval=y_tp[i], init_dist=Normal.dist(0, 100, shape=steps))
np.testing.assert_allclose(t0.compile_logp()(t0.initial_point()), t1.compile_logp()(t1.initial_point()))
beta_tp.set_value(np.full((ar_order,), 1 / ar_order))
init_dist = t0['y'].owner.inputs[2]
init_dist_tp = np.full((batch_size, ar_order), (np.arange(batch_size) * 100)[:, None])
y_eval = t0['y'].eval({init_dist: init_dist_tp})
assert y_eval.shape == (batch_size, steps + ar_order)
assert np.allclose(y_eval[:, -10:].mean(-1), np.arange(batch_size) * 100, rtol=0.1, atol=0.5)
```

## Next Steps


---

*Source: test_timeseries.py:627 | Complexity: Advanced | Last updated: 2026-05-18*