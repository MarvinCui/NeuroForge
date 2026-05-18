# How To: Sens Ic Vector 3 Params

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sens ic vector 3 params

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pymc`
- `pymc.ode`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign model5 = DifferentialEquation(...)

```python
model5 = DifferentialEquation(func=ode_func_5, t0=0, times=self.t, n_states=3, n_theta=3)
```

### Step 2: Assign model5_sens_ic = np.array(...)

```python
model5_sens_ic = np.array([[1, 0, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0], [0, 0, 1, 0, 0, 0]])
```

### Step 3: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(np.ravel(model5_sens_ic), model5._sens_ic)
```

### Step 4: Assign dx = value

```python
dx = p[0] * (y[1] - y[0])
```

### Step 5: Assign ds = value

```python
ds = y[0] * (p[1] - y[2]) - y[1]
```

### Step 6: Assign dz = value

```python
dz = y[0] * y[1] - p[2] * y[2]
```


## Complete Example

```python
# Workflow
def ode_func_5(y, t, p):
    dx = p[0] * (y[1] - y[0])
    ds = y[0] * (p[1] - y[2]) - y[1]
    dz = y[0] * y[1] - p[2] * y[2]
    return [dx, ds, dz]
model5 = DifferentialEquation(func=ode_func_5, t0=0, times=self.t, n_states=3, n_theta=3)
model5_sens_ic = np.array([[1, 0, 0, 0, 0, 0], [0, 1, 0, 0, 0, 0], [0, 0, 1, 0, 0, 0]])
np.testing.assert_array_equal(np.ravel(model5_sens_ic), model5._sens_ic)
```

## Next Steps


---

*Source: test_ode.py:132 | Complexity: Intermediate | Last updated: 2026-05-18*