# How To: Multiple Add Coords With Same Name

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multiple add coords with same name

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

### Step 1: Assign coord = value

```python
coord = {'dim1': ['a', 'b', 'c']}
```

**Verification:**
```python
assert len(variables) == 1 and variables[0] is m.dim_lengths['dim1']
```

### Step 2: Assign variables = get_var_by_name(...)

```python
variables = get_var_by_name([d], 'dim1')
```

**Verification:**
```python
assert len(variables) == 1 and variables[0] is m.dim_lengths['dim1']
```

### Step 3: Assign a = pm.Normal(...)

```python
a = pm.Normal('a', dims='dim1')
```

### Step 4: Call m.add_coords()

```python
m.add_coords(coord)
```

### Step 5: Assign c = pm.Normal(...)

```python
c = pm.Normal('c', dims='dim1')
```

### Step 6: Assign d = pm.Deterministic(...)

```python
d = pm.Deterministic('d', a + b + c)
```

### Step 7: Assign b = pm.Normal(...)

```python
b = pm.Normal('b', dims='dim1')
```


## Complete Example

```python
# Workflow
coord = {'dim1': ['a', 'b', 'c']}
with pm.Model(coords=coord) as m:
    a = pm.Normal('a', dims='dim1')
    with pm.Model(coords=coord) as nested_m:
        b = pm.Normal('b', dims='dim1')
    m.add_coords(coord)
    c = pm.Normal('c', dims='dim1')
    d = pm.Deterministic('d', a + b + c)
variables = get_var_by_name([d], 'dim1')
assert len(variables) == 1 and variables[0] is m.dim_lengths['dim1']
```

## Next Steps


---

*Source: test_core.py:860 | Complexity: Intermediate | Last updated: 2026-05-18*