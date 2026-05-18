# How To: Get Batched Jittered Initial Points

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test get batched jittered initial points

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

### Step 1: Assign ips = _get_batched_jittered_initial_points(...)

```python
ips = _get_batched_jittered_initial_points(model=model, chains=1, random_seed=1, initvals=None, jitter=False)
```

**Verification:**
```python
assert np.all(ips[0] == 0)
```

### Step 2: Assign ips = _get_batched_jittered_initial_points(...)

```python
ips = _get_batched_jittered_initial_points(model=model, chains=1, random_seed=1, initvals=None)
```

**Verification:**
```python
assert ips[0].shape == (2, 3)
```

### Step 3: Assign ips = _get_batched_jittered_initial_points(...)

```python
ips = _get_batched_jittered_initial_points(model=model, chains=2, random_seed=1, initvals=None)
```

**Verification:**
```python
assert np.all(ips[0] != 0)
```

### Step 4: Assign x = pm.MvNormal(...)

```python
x = pm.MvNormal('x', mu=np.zeros(3), cov=np.eye(3), shape=(2, 3), initval=np.zeros((2, 3)))
```

**Verification:**
```python
assert ips[0].shape == (2, 2, 3)
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    x = pm.MvNormal('x', mu=np.zeros(3), cov=np.eye(3), shape=(2, 3), initval=np.zeros((2, 3)))
ips = _get_batched_jittered_initial_points(model=model, chains=1, random_seed=1, initvals=None, jitter=False)
assert np.all(ips[0] == 0)
ips = _get_batched_jittered_initial_points(model=model, chains=1, random_seed=1, initvals=None)
assert ips[0].shape == (2, 3)
assert np.all(ips[0] != 0)
ips = _get_batched_jittered_initial_points(model=model, chains=2, random_seed=1, initvals=None)
assert ips[0].shape == (2, 2, 3)
assert np.all(ips[0][0] != ips[0][1])
```

## Next Steps


---

*Source: test_jax.py:308 | Complexity: Intermediate | Last updated: 2026-05-18*