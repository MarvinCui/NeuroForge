# How To: Datalogp Multiple Shapes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test datalogp multiple shapes

## Prerequisites

**Required Modules:**
- `copy`
- `pickle`
- `threading`
- `traceback`
- `warnings`
- `unittest.mock`
- `arviz`
- `cloudpickle`
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pytensor`
- `pytensor.sparse`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.sparse`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.graph.traversal`
- `pytensor.link.numba`
- `pytensor.raise_op`
- `pytensor.tensor.random.op`
- `pytensor.tensor.variable`
- `pymc`
- `pymc`
- `pymc.blocking`
- `pymc.distributions`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.exceptions`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.variational.minibatch_rv`
- `tests.models`


## Step-by-Step Guide

### Step 1: Assign x_val = value

```python
x_val = m.rvs_to_values[x]
```

### Step 2: Call m.datalogp.eval()

```python
m.datalogp.eval({x_val: 0})
```

### Step 3: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 0, 1)
```

### Step 4: Assign z1 = pm.Potential(...)

```python
z1 = pm.Potential('z1', x)
```

### Step 5: Assign z2 = pm.Potential(...)

```python
z2 = pm.Potential('z2', pt.full((1, 3), x))
```

### Step 6: Assign y1 = pm.Normal(...)

```python
y1 = pm.Normal('y1', x, 1, observed=np.array([1]))
```

### Step 7: Assign y2 = pm.Normal(...)

```python
y2 = pm.Normal('y2', x, 1, observed=np.array([1, 2]))
```

### Step 8: Assign y3 = pm.Normal(...)

```python
y3 = pm.Normal('y3', x, 1, observed=np.array([1, 2, 3]))
```


## Complete Example

```python
# Workflow
with pm.Model() as m:
    x = pm.Normal('x', 0, 1)
    z1 = pm.Potential('z1', x)
    z2 = pm.Potential('z2', pt.full((1, 3), x))
    y1 = pm.Normal('y1', x, 1, observed=np.array([1]))
    y2 = pm.Normal('y2', x, 1, observed=np.array([1, 2]))
    y3 = pm.Normal('y3', x, 1, observed=np.array([1, 2, 3]))
x_val = m.rvs_to_values[x]
m.datalogp.eval({x_val: 0})
```

## Next Steps


---

*Source: test_core.py:832 | Complexity: Advanced | Last updated: 2026-05-18*