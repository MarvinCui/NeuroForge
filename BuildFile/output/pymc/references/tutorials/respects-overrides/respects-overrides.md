# How To: Respects Overrides

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test respects overrides

## Prerequisites

**Required Modules:**
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.compile.builders`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc.distributions.distribution`
- `pymc.initial_point`


## Step-by-Step Guide

### Step 1: Assign fn = make_initial_point_fn(...)

```python
fn = make_initial_point_fn(model=pmodel, jitter_rvs={}, return_transformed=True, overrides={A: pt.as_tensor(2, dtype=int), B: 3, C: 5})
```

**Verification:**
```python
assert iv['A'] == 2
```

### Step 2: Assign iv = fn(...)

```python
iv = fn(0)
```

**Verification:**
```python
assert np.isclose(iv['B_log__'], np.log(3))
```

### Step 3: Assign A = pm.Flat(...)

```python
A = pm.Flat('A', initval='support_point')
```

**Verification:**
```python
assert iv['C'] == 5
```

### Step 4: Assign B = pm.HalfFlat(...)

```python
B = pm.HalfFlat('B', initval=4)
```

### Step 5: Assign C = pm.Normal(...)

```python
C = pm.Normal('C', mu=A + B, initval='support_point')
```


## Complete Example

```python
# Workflow
with pm.Model() as pmodel:
    A = pm.Flat('A', initval='support_point')
    B = pm.HalfFlat('B', initval=4)
    C = pm.Normal('C', mu=A + B, initval='support_point')
fn = make_initial_point_fn(model=pmodel, jitter_rvs={}, return_transformed=True, overrides={A: pt.as_tensor(2, dtype=int), B: 3, C: 5})
iv = fn(0)
assert iv['A'] == 2
assert np.isclose(iv['B_log__'], np.log(3))
assert iv['C'] == 5
```

## Next Steps


---

*Source: test_initial_point.py:164 | Complexity: Intermediate | Last updated: 2026-05-18*