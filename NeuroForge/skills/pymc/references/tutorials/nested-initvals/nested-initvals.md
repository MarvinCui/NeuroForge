# How To: Nested Initvals

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nested initvals

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

### Step 1: Assign ip_vals = list(...)

```python
ip_vals = list(make_initial_point_fn(model=pmodel, return_transformed=True)(0).values())
```

**Verification:**
```python
assert np.allclose(np.exp(ip_vals), [1, 2, 4, 8, 16, 32], rtol=0.001)
```

### Step 2: Assign ip_vals = list(...)

```python
ip_vals = list(make_initial_point_fn(model=pmodel, return_transformed=False)(0).values())
```

**Verification:**
```python
assert np.allclose(ip_vals, [1, 2, 4, 8, 16, 32], rtol=0.001)
```

### Step 3: Assign unknown = 1

```python
pmodel.rvs_to_initial_values[four] = 1
```

**Verification:**
```python
assert np.allclose(np.exp(ip_vals), [1, 2, 4, 1, 2, 4], rtol=0.001)
```

### Step 4: Assign ip_vals = list(...)

```python
ip_vals = list(make_initial_point_fn(model=pmodel, return_transformed=True)(0).values())
```

**Verification:**
```python
assert np.allclose(ip_vals, [1, 2, 4, 1, 2, 4], rtol=0.001)
```

### Step 5: Assign ip_vals = list(...)

```python
ip_vals = list(make_initial_point_fn(model=pmodel, return_transformed=False)(0).values())
```

**Verification:**
```python
assert np.allclose(ip_vals, [1, 2, 4, 1, 2, 4], rtol=0.001)
```

### Step 6: Assign one = pm.LogNormal(...)

```python
one = pm.LogNormal('one', mu=np.log(1), sigma=1e-05, initval='prior')
```

### Step 7: Assign two = pm.Lognormal(...)

```python
two = pm.Lognormal('two', mu=np.log(one * 2), sigma=1e-05, initval='prior')
```

### Step 8: Assign three = pm.LogNormal(...)

```python
three = pm.LogNormal('three', mu=np.log(two * 2), sigma=1e-05, initval='prior')
```

### Step 9: Assign four = pm.LogNormal(...)

```python
four = pm.LogNormal('four', mu=np.log(three * 2), sigma=1e-05, initval='prior')
```

### Step 10: Assign five = pm.LogNormal(...)

```python
five = pm.LogNormal('five', mu=np.log(four * 2), sigma=1e-05, initval='prior')
```

### Step 11: Assign six = pm.LogNormal(...)

```python
six = pm.LogNormal('six', mu=np.log(five * 2), sigma=1e-05, initval='prior')
```


## Complete Example

```python
# Workflow
with pm.Model() as pmodel:
    one = pm.LogNormal('one', mu=np.log(1), sigma=1e-05, initval='prior')
    two = pm.Lognormal('two', mu=np.log(one * 2), sigma=1e-05, initval='prior')
    three = pm.LogNormal('three', mu=np.log(two * 2), sigma=1e-05, initval='prior')
    four = pm.LogNormal('four', mu=np.log(three * 2), sigma=1e-05, initval='prior')
    five = pm.LogNormal('five', mu=np.log(four * 2), sigma=1e-05, initval='prior')
    six = pm.LogNormal('six', mu=np.log(five * 2), sigma=1e-05, initval='prior')
ip_vals = list(make_initial_point_fn(model=pmodel, return_transformed=True)(0).values())
assert np.allclose(np.exp(ip_vals), [1, 2, 4, 8, 16, 32], rtol=0.001)
ip_vals = list(make_initial_point_fn(model=pmodel, return_transformed=False)(0).values())
assert np.allclose(ip_vals, [1, 2, 4, 8, 16, 32], rtol=0.001)
pmodel.rvs_to_initial_values[four] = 1
ip_vals = list(make_initial_point_fn(model=pmodel, return_transformed=True)(0).values())
assert np.allclose(np.exp(ip_vals), [1, 2, 4, 1, 2, 4], rtol=0.001)
ip_vals = list(make_initial_point_fn(model=pmodel, return_transformed=False)(0).values())
assert np.allclose(ip_vals, [1, 2, 4, 1, 2, 4], rtol=0.001)
```

## Next Steps


---

*Source: test_initial_point.py:84 | Complexity: Advanced | Last updated: 2026-05-18*