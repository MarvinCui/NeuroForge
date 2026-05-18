# How To: Multiple Simulators

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multiple simulators

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

### Step 2: Assign true_b = value

```python
true_b = -2
```

**Verification:**
```python
assert any((node for node in logp_sim1_fn.maker.fgraph.toposort() if isinstance(node.op, SortOp)))
```

### Step 3: Assign data1 = np.random.normal(...)

```python
data1 = np.random.normal(true_a, 0.1, size=1000)
```

**Verification:**
```python
assert not any((node for node in logp_sim2_fn.maker.fgraph.toposort() if isinstance(node.op, SortOp)))
```

### Step 4: Assign data2 = np.random.normal(...)

```python
data2 = np.random.normal(true_b, 0.1, size=1000)
```

**Verification:**
```python
assert abs(true_a - trace['a'].mean()) < 0.05
```

### Step 5: Assign logp_sim1_fn = m.compile_fn(...)

```python
logp_sim1_fn = m.compile_fn(m.logp(sim1), point_fn=False)
```

**Verification:**
```python
assert abs(true_b - trace['b'].mean()) < 0.05
```

### Step 6: Assign logp_sim2_fn = m.compile_fn(...)

```python
logp_sim2_fn = m.compile_fn(m.logp(sim2), point_fn=False)
```

**Verification:**
```python
assert any((node for node in logp_sim1_fn.maker.fgraph.toposort() if isinstance(node.op, SortOp)))
```

### Step 7: Assign a = pm.Normal(...)

```python
a = pm.Normal('a', mu=0, sigma=3)
```

### Step 8: Assign b = pm.Normal(...)

```python
b = pm.Normal('b', mu=0, sigma=3)
```

### Step 9: Assign sim1 = pm.Simulator(...)

```python
sim1 = pm.Simulator('sim1', self.normal_sim, a, 0.1, distance='gaussian', sum_stat='sort', observed=data1)
```

### Step 10: Assign sim2 = pm.Simulator(...)

```python
sim2 = pm.Simulator('sim2', self.normal_sim, b, 0.1, distance='laplace', sum_stat='mean', epsilon=0.1, observed=data2)
```

### Step 11: Assign trace = pm.sample_smc(...)

```python
trace = pm.sample_smc(return_inferencedata=False)
```


## Complete Example

```python
# Setup
# Fixtures: seeded_test

# Workflow
true_a = 2
true_b = -2
data1 = np.random.normal(true_a, 0.1, size=1000)
data2 = np.random.normal(true_b, 0.1, size=1000)
with pm.Model() as m:
    a = pm.Normal('a', mu=0, sigma=3)
    b = pm.Normal('b', mu=0, sigma=3)
    sim1 = pm.Simulator('sim1', self.normal_sim, a, 0.1, distance='gaussian', sum_stat='sort', observed=data1)
    sim2 = pm.Simulator('sim2', self.normal_sim, b, 0.1, distance='laplace', sum_stat='mean', epsilon=0.1, observed=data2)
assert self.count_rvs(m.logp()) == 2
logp_sim1_fn = m.compile_fn(m.logp(sim1), point_fn=False)
logp_sim2_fn = m.compile_fn(m.logp(sim2), point_fn=False)
assert any((node for node in logp_sim1_fn.maker.fgraph.toposort() if isinstance(node.op, SortOp)))
assert not any((node for node in logp_sim2_fn.maker.fgraph.toposort() if isinstance(node.op, SortOp)))
with m:
    trace = pm.sample_smc(return_inferencedata=False)
assert abs(true_a - trace['a'].mean()) < 0.05
assert abs(true_b - trace['b'].mean()) < 0.05
```

## Next Steps


---

*Source: test_simulator.py:177 | Complexity: Advanced | Last updated: 2026-05-18*