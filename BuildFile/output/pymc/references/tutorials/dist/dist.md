# How To: Dist

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dist

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.link.numba`
- `pytensor.tensor.random.op`
- `pytensor.tensor.random.variable`
- `pytensor.tensor.sort`
- `pymc`
- `pymc.initial_point`
- `pymc.pytensorf`
- `pymc.smc.kernels`

**Setup Required:**
```python
# Fixtures: seeded_test
```

## Step-by-Step Guide

### Step 1: Assign x = pm.Simulator.dist(...)

```python
x = pm.Simulator.dist(self.normal_sim, 0, 1, sum_stat='sort', shape=(3,))
```

**Verification:**
```python
assert res1.shape == (3,)
```

### Step 2: Assign x = cloudpickle.loads(...)

```python
x = cloudpickle.loads(cloudpickle.dumps(x))
```

**Verification:**
```python
assert np.all(res1 != res2)
```

### Step 3: Assign x_logp = pm.logp(...)

```python
x_logp = pm.logp(x, [0, 1, 2])
```

**Verification:**
```python
assert np.all(res1 == res3)
```

### Step 4: Assign x_logp_fn = compile(...)

```python
x_logp_fn = compile([], x_logp, random_seed=1)
```

**Verification:**
```python
assert np.all(res2 == res4)
```

### Step 5: Assign unknown = value

```python
res1, res2 = (x_logp_fn(), x_logp_fn())
```

**Verification:**
```python
assert res1.shape == (3,)
```

### Step 6: Assign x_logp_fn = compile(...)

```python
x_logp_fn = compile([], x_logp, random_seed=1)
```

### Step 7: Assign unknown = value

```python
res3, res4 = (x_logp_fn(), x_logp_fn())
```

**Verification:**
```python
assert np.all(res1 == res3)
```


## Complete Example

```python
# Setup
# Fixtures: seeded_test

# Workflow
x = pm.Simulator.dist(self.normal_sim, 0, 1, sum_stat='sort', shape=(3,))
x = cloudpickle.loads(cloudpickle.dumps(x))
x_logp = pm.logp(x, [0, 1, 2])
x_logp_fn = compile([], x_logp, random_seed=1)
res1, res2 = (x_logp_fn(), x_logp_fn())
assert res1.shape == (3,)
assert np.all(res1 != res2)
x_logp_fn = compile([], x_logp, random_seed=1)
res3, res4 = (x_logp_fn(), x_logp_fn())
assert np.all(res1 == res3)
assert np.all(res2 == res4)
```

## Next Steps


---

*Source: test_simulator.py:370 | Complexity: Intermediate | Last updated: 2026-05-18*