# How To: Sens Ic Vector 2 Param

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sens ic vector 2 param

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

### Step 1: Assign model4 = DifferentialEquation(...)

```python
model4 = DifferentialEquation(func=ode_func_4, t0=0, times=self.t, n_states=2, n_theta=2)
```

### Step 2: Assign model4_sens_ic = np.array(...)

```python
model4_sens_ic = np.array([1, 0, 0, 0, 0, 1, 0, 0])
```

### Step 3: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(model4_sens_ic, model4._sens_ic)
```

### Step 4: Assign ds = value

```python
ds = -p[0] * y[0] * y[1]
```

### Step 5: Assign di = value

```python
di = p[0] * y[0] * y[1] - p[1] * y[1]
```


## Complete Example

```python
# Workflow
def ode_func_4(y, t, p):
    ds = -p[0] * y[0] * y[1]
    di = p[0] * y[0] * y[1] - p[1] * y[1]
    return [ds, di]
model4 = DifferentialEquation(func=ode_func_4, t0=0, times=self.t, n_states=2, n_theta=2)
model4_sens_ic = np.array([1, 0, 0, 0, 0, 1, 0, 0])
np.testing.assert_array_equal(model4_sens_ic, model4._sens_ic)
```

## Next Steps


---

*Source: test_ode.py:99 | Complexity: Intermediate | Last updated: 2026-05-18*