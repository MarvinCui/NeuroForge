# How To: Nested Model Coords

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nested model coords

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

### Step 1: Assign a = pm.Normal(...)

```python
a = pm.Normal('a', dims='dim1')
```

**Verification:**
```python
assert m1.coords is m2.coords
```

### Step 2: Assign e = pm.Normal(...)

```python
e = pm.Normal('e', a[None] + d[:, None], dims=('dim2', 'dim1'))
```

**Verification:**
```python
assert m1.dim_lengths is m2.dim_lengths
```

### Step 3: Assign b = pm.Normal(...)

```python
b = pm.Normal('b', dims='dim1')
```

**Verification:**
```python
assert set(m2.named_vars_to_dims) < set(m1.named_vars_to_dims)
```

### Step 4: Call m1.add_coord()

```python
m1.add_coord('dim3', range(4))
```

### Step 5: Assign c = pm.HalfNormal(...)

```python
c = pm.HalfNormal('c', dims='dim3')
```

### Step 6: Assign d = pm.Normal(...)

```python
d = pm.Normal('d', b, c, dims='dim2')
```


## Complete Example

```python
# Workflow
with pm.Model(name='m1', coords={'dim1': range(2)}) as m1:
    a = pm.Normal('a', dims='dim1')
    with pm.Model(name='m2', coords={'dim2': range(4)}) as m2:
        b = pm.Normal('b', dims='dim1')
        m1.add_coord('dim3', range(4))
        c = pm.HalfNormal('c', dims='dim3')
        d = pm.Normal('d', b, c, dims='dim2')
    e = pm.Normal('e', a[None] + d[:, None], dims=('dim2', 'dim1'))
assert m1.coords is m2.coords
assert m1.dim_lengths is m2.dim_lengths
assert set(m2.named_vars_to_dims) < set(m1.named_vars_to_dims)
```

## Next Steps


---

*Source: test_core.py:846 | Complexity: Intermediate | Last updated: 2026-05-18*