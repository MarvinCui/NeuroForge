# How To: Sens Ic Vector 1 Param

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sens ic vector 1 param

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

### Step 1: Assign model3 = DifferentialEquation(...)

```python
model3 = DifferentialEquation(func=ode_func_3, t0=0, times=self.t, n_states=2, n_theta=1)
```

### Step 2: Assign model3_sens_ic = np.array(...)

```python
model3_sens_ic = np.array([1, 0, 0, 0, 1, 0])
```

### Step 3: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(model3_sens_ic, model3._sens_ic)
```

### Step 4: Assign ds = value

```python
ds = -p[0] * y[0] * y[1]
```

### Step 5: Assign di = value

```python
di = p[0] * y[0] * y[1] - y[1]
```


## Complete Example

```python
# Workflow
def ode_func_3(y, t, p):
    ds = -p[0] * y[0] * y[1]
    di = p[0] * y[0] * y[1] - y[1]
    return [ds, di]
model3 = DifferentialEquation(func=ode_func_3, t0=0, times=self.t, n_states=2, n_theta=1)
model3_sens_ic = np.array([1, 0, 0, 0, 1, 0])
np.testing.assert_array_equal(model3_sens_ic, model3._sens_ic)
```

## Next Steps


---

*Source: test_ode.py:84 | Complexity: Intermediate | Last updated: 2026-05-18*