# How To: Symbolic Normalizing Constant No Rvs

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test symbolic normalizing constant no rvs

## Prerequisites

**Required Modules:**
- `functools`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.testing`
- `pymc.variational`
- `pymc.variational.approximations`
- `tests.helpers`
- `cloudpickle`
- `cloudpickle`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng()
```

**Verification:**
```python
assert_no_rvs(step.approx.symbolic_normalizing_constant)
```

### Step 2: Call assert_no_rvs()

```python
assert_no_rvs(step.approx.symbolic_normalizing_constant)
```

### Step 3: Assign obs = pm.Data(...)

```python
obs = pm.Data('obs', rng.normal(size=(1000,)))
```

### Step 4: Assign obs_batch = pm.Minibatch(...)

```python
obs_batch = pm.Minibatch(obs, batch_size=128)
```

### Step 5: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

### Step 6: Assign y_hat = pm.Flat(...)

```python
y_hat = pm.Flat('y_hat', observed=obs_batch, total_size=1000)
```

### Step 7: Assign step = pm.ADVI(...)

```python
step = pm.ADVI()
```


## Complete Example

```python
# Workflow
rng = np.random.default_rng()
with pm.Model() as m:
    obs = pm.Data('obs', rng.normal(size=(1000,)))
    obs_batch = pm.Minibatch(obs, batch_size=128)
    x = pm.Normal('x')
    y_hat = pm.Flat('y_hat', observed=obs_batch, total_size=1000)
    step = pm.ADVI()
assert_no_rvs(step.approx.symbolic_normalizing_constant)
```

## Next Steps


---

*Source: test_opvi.py:287 | Complexity: Intermediate | Last updated: 2026-05-18*