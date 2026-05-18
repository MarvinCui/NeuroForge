# How To: Do Dims

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test do dims

## Prerequisites

**Required Modules:**
- `arviz`
- `numpy`
- `pytest`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.variational.minibatch_rv`


## Step-by-Step Guide

### Step 1: Assign coords = value

```python
coords = {'test_dim': range(10)}
```

**Verification:**
```python
assert do_m.named_vars_to_dims['x'] == ['test_dim']
```

### Step 2: Assign do_m = do(...)

```python
do_m = do(m, {'x': np.zeros(10, dtype=config.floatX)})
```

**Verification:**
```python
assert do_m.named_vars_to_dims['y'] == ['test_dim']
```

### Step 3: Assign do_m = do(...)

```python
do_m = do(m, {'y': np.zeros(10, dtype=config.floatX)})
```

**Verification:**
```python
assert do_m.named_vars_to_dims['y'] == ['test_dim']
```

### Step 4: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', dims='test_dim')
```

### Step 5: Assign y = pm.Deterministic(...)

```python
y = pm.Deterministic('y', x + 5, dims='test_dim')
```


## Complete Example

```python
# Workflow
coords = {'test_dim': range(10)}
with pm.Model(coords=coords) as m:
    x = pm.Normal('x', dims='test_dim')
    y = pm.Deterministic('y', x + 5, dims='test_dim')
do_m = do(m, {'x': np.zeros(10, dtype=config.floatX)})
assert do_m.named_vars_to_dims['x'] == ['test_dim']
do_m = do(m, {'y': np.zeros(10, dtype=config.floatX)})
assert do_m.named_vars_to_dims['y'] == ['test_dim']
```

## Next Steps


---

*Source: test_conditioning.py:222 | Complexity: Intermediate | Last updated: 2026-05-18*