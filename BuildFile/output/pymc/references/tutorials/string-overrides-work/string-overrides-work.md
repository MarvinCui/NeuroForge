# How To: String Overrides Work

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test string overrides work

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
fn = make_initial_point_fn(model=pmodel, jitter_rvs={}, return_transformed=True, overrides={'A': 1, 'B': 1, 'C_log__': 0})
```

**Verification:**
```python
assert iv['A'] == 1
```

### Step 2: Assign iv = fn(...)

```python
iv = fn(0)
```

**Verification:**
```python
assert np.isclose(iv['B_log__'], 0)
```

### Step 3: Assign A = pm.Flat(...)

```python
A = pm.Flat('A', initval=10)
```

**Verification:**
```python
assert iv['C_log__'] == 0
```

### Step 4: Assign B = pm.HalfFlat(...)

```python
B = pm.HalfFlat('B', initval=10)
```

### Step 5: Assign C = pm.HalfFlat(...)

```python
C = pm.HalfFlat('C', initval=10)
```


## Complete Example

```python
# Workflow
with pm.Model() as pmodel:
    A = pm.Flat('A', initval=10)
    B = pm.HalfFlat('B', initval=10)
    C = pm.HalfFlat('C', initval=10)
fn = make_initial_point_fn(model=pmodel, jitter_rvs={}, return_transformed=True, overrides={'A': 1, 'B': 1, 'C_log__': 0})
iv = fn(0)
assert iv['A'] == 1
assert np.isclose(iv['B_log__'], 0)
assert iv['C_log__'] == 0
```

## Next Steps


---

*Source: test_initial_point.py:184 | Complexity: Intermediate | Last updated: 2026-05-18*