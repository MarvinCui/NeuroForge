# How To: Freeze Dim After Do Intervention

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test freeze dim after do intervention

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc.data`
- `pymc.distributions`
- `pymc.exceptions`
- `pymc.model`
- `pymc.model.transform.optimization`
- `pymc.pytensorf`


## Step-by-Step Guide

### Step 1: Assign do_m = do(...)

```python
do_m = do(m, {mu: mu * 100})
```

**Verification:**
```python
assert do_m['x'].type.shape == (None,)
```

### Step 2: Assign frozen_do_m = freeze_dims_and_data(...)

```python
frozen_do_m = freeze_dims_and_data(do_m)
```

**Verification:**
```python
assert frozen_do_m['x'].type.shape == (5,)
```

### Step 3: Assign mu = Data(...)

```python
mu = Data('mu', [0, 1, 2, 3, 4], dims='test_dim')
```

### Step 4: Assign x = Normal(...)

```python
x = Normal('x', mu=mu, dims='test_dim')
```


## Complete Example

```python
# Workflow
with Model(coords={'test_dim': range(5)}) as m:
    mu = Data('mu', [0, 1, 2, 3, 4], dims='test_dim')
    x = Normal('x', mu=mu, dims='test_dim')
do_m = do(m, {mu: mu * 100})
assert do_m['x'].type.shape == (None,)
frozen_do_m = freeze_dims_and_data(do_m)
assert frozen_do_m['x'].type.shape == (5,)
```

## Next Steps


---

*Source: test_optimization.py:139 | Complexity: Intermediate | Last updated: 2026-05-18*