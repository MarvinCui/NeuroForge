# How To: Adds Jitter

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test adds jitter

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
fn = make_initial_point_fn(model=pmodel, jitter_rvs={B}, return_transformed=True)
```

**Verification:**
```python
assert iv['A'] == 0
```

### Step 2: Assign iv = fn(...)

```python
iv = fn(0)
```

**Verification:**
```python
assert b_transformed != 0
```

### Step 3: Assign b_transformed = value

```python
b_transformed = iv['B_log__']
```

**Verification:**
```python
assert -1 < b_transformed < 1
```

### Step 4: Assign b_untransformed = transform_back(...)

```python
b_untransformed = transform_back(B, b_transformed, model=pmodel)
```

**Verification:**
```python
assert np.isclose(iv['C'], np.array(0 + b_untransformed, dtype=pytensor.config.floatX))
```

### Step 5: Assign A = pm.Flat(...)

```python
A = pm.Flat('A', initval='support_point')
```

**Verification:**
```python
assert fn(0) == fn(0)
```

### Step 6: Assign B = pm.HalfFlat(...)

```python
B = pm.HalfFlat('B', initval='support_point')
```

**Verification:**
```python
assert fn(0) != fn(1)
```

### Step 7: Assign C = pm.Normal(...)

```python
C = pm.Normal('C', mu=A + B, initval='support_point')
```


## Complete Example

```python
# Workflow
with pm.Model() as pmodel:
    A = pm.Flat('A', initval='support_point')
    B = pm.HalfFlat('B', initval='support_point')
    C = pm.Normal('C', mu=A + B, initval='support_point')
fn = make_initial_point_fn(model=pmodel, jitter_rvs={B}, return_transformed=True)
iv = fn(0)
assert iv['A'] == 0
b_transformed = iv['B_log__']
b_untransformed = transform_back(B, b_transformed, model=pmodel)
assert b_transformed != 0
assert -1 < b_transformed < 1
assert np.isclose(iv['C'], np.array(0 + b_untransformed, dtype=pytensor.config.floatX))
assert fn(0) == fn(0)
assert fn(0) != fn(1)
```

## Next Steps


---

*Source: test_initial_point.py:143 | Complexity: Intermediate | Last updated: 2026-05-18*