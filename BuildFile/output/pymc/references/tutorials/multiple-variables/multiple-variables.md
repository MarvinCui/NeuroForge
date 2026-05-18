# How To: Multiple Variables

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multiple variables

## Prerequisites

**Required Modules:**
- `logging`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `arviz_base`
- `arviz_base.testing`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pytensor.graph.traversal`
- `pytensor.tensor.variable`
- `scipy`
- `pymc`
- `pymc.backends.base`
- `pymc.distributions.shape_utils`
- `pymc.exceptions`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign num_draws = 100

```python
num_draws = 100
```

**Verification:**
```python
assert draws[0].shape == (num_draws,)
```

### Step 2: Assign draws = pm.draw(...)

```python
draws = pm.draw((x, y, z, w), draws=num_draws)
```

**Verification:**
```python
assert draws[1].shape == (num_draws, 10)
```

### Step 3: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

**Verification:**
```python
assert draws[2].shape == (num_draws, 5)
```

### Step 4: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', shape=10)
```

**Verification:**
```python
assert draws[3].shape == (num_draws, 3)
```

### Step 5: Assign z = pm.Uniform(...)

```python
z = pm.Uniform('z', shape=5)
```

### Step 6: Assign w = pm.Dirichlet(...)

```python
w = pm.Dirichlet('w', a=[1, 1, 1])
```


## Complete Example

```python
# Workflow
with pm.Model():
    x = pm.Normal('x')
    y = pm.Normal('y', shape=10)
    z = pm.Uniform('z', shape=5)
    w = pm.Dirichlet('w', a=[1, 1, 1])
num_draws = 100
draws = pm.draw((x, y, z, w), draws=num_draws)
assert draws[0].shape == (num_draws,)
assert draws[1].shape == (num_draws, 10)
assert draws[2].shape == (num_draws, 5)
assert draws[3].shape == (num_draws, 3)
```

## Next Steps


---

*Source: test_forward.py:87 | Complexity: Intermediate | Last updated: 2026-05-18*