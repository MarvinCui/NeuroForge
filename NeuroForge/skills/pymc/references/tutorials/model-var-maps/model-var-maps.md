# How To: Model Var Maps

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test model var maps

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

### Step 1: Assign a_value = value

```python
a_value = model.rvs_to_values[a]
```

**Verification:**
```python
assert set(model.rvs_to_values.keys()) == {a, x}
```

### Step 2: Assign x_value = value

```python
x_value = model.rvs_to_values[x]
```

**Verification:**
```python
assert a_value.owner is None
```

### Step 3: Assign a = pm.Uniform(...)

```python
a = pm.Uniform('a')
```

**Verification:**
```python
assert x_value.owner is None
```

### Step 4: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', a)
```

**Verification:**
```python
assert model.values_to_rvs == {a_value: a, x_value: x}
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    a = pm.Uniform('a')
    x = pm.Normal('x', a)
assert set(model.rvs_to_values.keys()) == {a, x}
a_value = model.rvs_to_values[a]
x_value = model.rvs_to_values[x]
assert a_value.owner is None
assert x_value.owner is None
assert model.values_to_rvs == {a_value: a, x_value: x}
assert set(model.rvs_to_transforms.keys()) == {a, x}
assert isinstance(model.rvs_to_transforms[a], IntervalTransform)
assert model.rvs_to_transforms[x] is None
```

## Next Steps


---

*Source: test_core.py:583 | Complexity: Intermediate | Last updated: 2026-05-18*