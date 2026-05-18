# How To: Interval Near Boundary

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test interval near boundary

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.pytensorf`
- `pymc.testing`
- `numpy`


## Step-by-Step Guide

### Step 1: Assign lb = value

```python
lb = -1.0
```

**Verification:**
```python
assert_allclose(list(log_prob.values()), floatX(np.array([-52.68])))
```

### Step 2: Assign ub = 1e-07

```python
ub = 1e-07
```

### Step 3: Assign x0 = np.nextafter(...)

```python
x0 = np.nextafter(ub, lb)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(list(log_prob.values()), floatX(np.array([-52.68])))
```

### Step 5: Call pm.Uniform()

```python
pm.Uniform('x', initval=x0, lower=lb, upper=ub)
```

### Step 6: Assign log_prob = model.point_logps(...)

```python
log_prob = model.point_logps()
```


## Complete Example

```python
# Workflow
lb = -1.0
ub = 1e-07
x0 = np.nextafter(ub, lb)
with pm.Model() as model:
    pm.Uniform('x', initval=x0, lower=lb, upper=ub)
with config.change_flags(numba__fastmath=False):
    log_prob = model.point_logps()
assert_allclose(list(log_prob.values()), floatX(np.array([-52.68])))
```

## Next Steps


---

*Source: test_transform.py:229 | Complexity: Intermediate | Last updated: 2026-05-18*