# How To: Nested Simulators

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nested simulators

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

### Step 1: Assign true_a = 2

```python
true_a = 2
```

**Verification:**
```python
assert self.count_rvs(m.logp()) == 2
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(20160911)
```

**Verification:**
```python
assert np.abs(true_a - trace['sim1'].mean()) < 0.1
```

### Step 3: Assign data = rng.normal(...)

```python
data = rng.normal(true_a, 0.1, size=1000)
```

**Verification:**
```python
assert self.count_rvs(m.logp()) == 2
```

### Step 4: Assign sim1 = pm.Simulator(...)

```python
sim1 = pm.Simulator('sim1', self.normal_sim, params=(0, 4), distance='gaussian', sum_stat='identity')
```

### Step 5: Assign sim2 = pm.Simulator(...)

```python
sim2 = pm.Simulator('sim2', self.normal_sim, params=(sim1, 0.1), distance='gaussian', sum_stat='mean', epsilon=0.1, observed=data)
```

### Step 6: Assign trace = pm.sample_smc(...)

```python
trace = pm.sample_smc(return_inferencedata=False)
```


## Complete Example

```python
# Setup
# Fixtures: seeded_test

# Workflow
true_a = 2
rng = np.random.RandomState(20160911)
data = rng.normal(true_a, 0.1, size=1000)
with pm.Model() as m:
    sim1 = pm.Simulator('sim1', self.normal_sim, params=(0, 4), distance='gaussian', sum_stat='identity')
    sim2 = pm.Simulator('sim2', self.normal_sim, params=(sim1, 0.1), distance='gaussian', sum_stat='mean', epsilon=0.1, observed=data)
assert self.count_rvs(m.logp()) == 2
with m:
    trace = pm.sample_smc(return_inferencedata=False)
assert np.abs(true_a - trace['sim1'].mean()) < 0.1
```

## Next Steps


---

*Source: test_simulator.py:227 | Complexity: Intermediate | Last updated: 2026-05-18*