# How To: Batched Size

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test batched size

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: constant
```

## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
ar_order, steps, batch_size = (3, 100, 5)
```

**Verification:**
```python
assert y.owner.op.ar_order == ar_order
```

### Step 2: Assign beta_tp = np.random.randn(...)

```python
beta_tp = np.random.randn(batch_size, ar_order + int(constant))
```

**Verification:**
```python
assert y_eval[0].shape == (batch_size, steps)
```

### Step 3: Assign y_tp = np.random.randn(...)

```python
y_tp = np.random.randn(batch_size, steps)
```

**Verification:**
```python
assert not np.any(np.isclose(y_eval[0], y_eval[1]))
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(t0.compile_logp()(t0.initial_point()), t1.compile_logp()(t1.initial_point()))
```

### Step 5: Assign y_eval = draw(...)

```python
y_eval = draw(y, draws=2)
```

**Verification:**
```python
assert y_eval[0].shape == (batch_size, steps)
```

### Step 6: Assign y = AR(...)

```python
y = AR('y', beta_tp, shape=(batch_size, steps), initval=y_tp, constant=constant, init_dist=Normal.dist(0, 100, shape=(batch_size, steps)))
```

### Step 7: Call AR()

```python
AR(f'y_{i}', beta_tp[i], sigma=1.0, shape=steps, initval=y_tp[i], constant=constant, init_dist=Normal.dist(0, 100, shape=steps))
```


## Complete Example

```python
# Setup
# Fixtures: constant

# Workflow
ar_order, steps, batch_size = (3, 100, 5)
beta_tp = np.random.randn(batch_size, ar_order + int(constant))
y_tp = np.random.randn(batch_size, steps)
with Model() as t0:
    y = AR('y', beta_tp, shape=(batch_size, steps), initval=y_tp, constant=constant, init_dist=Normal.dist(0, 100, shape=(batch_size, steps)))
with Model() as t1:
    for i in range(batch_size):
        AR(f'y_{i}', beta_tp[i], sigma=1.0, shape=steps, initval=y_tp[i], constant=constant, init_dist=Normal.dist(0, 100, shape=steps))
assert y.owner.op.ar_order == ar_order
np.testing.assert_allclose(t0.compile_logp()(t0.initial_point()), t1.compile_logp()(t1.initial_point()))
y_eval = draw(y, draws=2)
assert y_eval[0].shape == (batch_size, steps)
assert not np.any(np.isclose(y_eval[0], y_eval[1]))
```

## Next Steps


---

*Source: test_timeseries.py:507 | Complexity: Intermediate | Last updated: 2026-05-18*