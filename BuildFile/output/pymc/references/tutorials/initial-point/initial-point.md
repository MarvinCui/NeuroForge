# How To: Initial Point

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test initial point

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

### Step 1: Assign b_initval = np.array(...)

```python
b_initval = np.array(0.3, dtype=pytensor.config.floatX)
```

**Verification:**
```python
assert a in model.rvs_to_initial_values
```

### Step 2: Assign b_initval_trans = unknown.forward.eval(...)

```python
b_initval_trans = model.rvs_to_transforms[b].forward(b_initval, *b.owner.inputs).eval()
```

**Verification:**
```python
assert x in model.rvs_to_initial_values
```

### Step 3: Assign y_initval = np.array(...)

```python
y_initval = np.array(-2.4, dtype=pytensor.config.floatX)
```

**Verification:**
```python
assert model.rvs_to_initial_values[b] == b_initval
```

### Step 4: Assign a = pm.Uniform(...)

```python
a = pm.Uniform('a')
```

**Verification:**
```python
assert model.initial_point(0)['b_interval__'] == b_initval_trans
```

### Step 5: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', a)
```

**Verification:**
```python
assert model.rvs_to_initial_values[y] == y_initval
```

### Step 6: Assign b = pm.Uniform(...)

```python
b = pm.Uniform('b', initval=b_initval)
```

### Step 7: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', initval=y_initval)
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    a = pm.Uniform('a')
    x = pm.Normal('x', a)
b_initval = np.array(0.3, dtype=pytensor.config.floatX)
with model:
    b = pm.Uniform('b', initval=b_initval)
b_initval_trans = model.rvs_to_transforms[b].forward(b_initval, *b.owner.inputs).eval()
y_initval = np.array(-2.4, dtype=pytensor.config.floatX)
with model:
    y = pm.Normal('y', initval=y_initval)
assert a in model.rvs_to_initial_values
assert x in model.rvs_to_initial_values
assert model.rvs_to_initial_values[b] == b_initval
assert model.initial_point(0)['b_interval__'] == b_initval_trans
assert model.rvs_to_initial_values[y] == y_initval
```

## Next Steps


---

*Source: test_core.py:690 | Complexity: Intermediate | Last updated: 2026-05-18*