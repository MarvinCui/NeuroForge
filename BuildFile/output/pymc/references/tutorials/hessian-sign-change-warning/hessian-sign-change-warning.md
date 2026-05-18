# How To: Hessian Sign Change Warning

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test hessian sign change warning

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pandas`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.sparse`
- `pytensor`
- `pytensor.compile`
- `pytensor.compile.builders`
- `pytensor.graph.basic`
- `pytensor.link.vm`
- `pytensor.tensor.subtensor`
- `pymc`
- `pymc.data`
- `pymc.distributions.dist_math`
- `pymc.distributions.distribution`
- `pymc.exceptions`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.vartypes`
- `cloudpickle`

**Setup Required:**
```python
# Fixtures: func
```

## Step-by-Step Guide

### Step 1: Assign x = pt.vector(...)

```python
x = pt.vector('x')
```

**Verification:**
```python
assert equal_computations([res_neg], [-res])
```

### Step 2: Assign f = unknown.sum(...)

```python
f = (x ** 2).sum()
```

### Step 3: Assign res = func(...)

```python
res = func(f, vars=[x], negate_output=False)
```

**Verification:**
```python
assert equal_computations([res_neg], [-res])
```

### Step 4: Assign res_neg = func(...)

```python
res_neg = func(f, vars=[x])
```


## Complete Example

```python
# Setup
# Fixtures: func

# Workflow
x = pt.vector('x')
f = (x ** 2).sum()
with pytest.warns(FutureWarning, match='will stop negating the output'):
    res_neg = func(f, vars=[x])
res = func(f, vars=[x], negate_output=False)
assert equal_computations([res_neg], [-res])
```

## Next Steps


---

*Source: test_pytensorf.py:750 | Complexity: Intermediate | Last updated: 2026-05-18*