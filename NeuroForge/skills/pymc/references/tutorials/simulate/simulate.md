# How To: Simulate

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests the integration in DifferentialEquation

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

### Step 1: 'Tests the integration in DifferentialEquation'

```python
'Tests the integration in DifferentialEquation'
```

**Verification:**
```python
assert simulated_y.shape == (len(t), 1)
```

### Step 2: Assign y0 = 0

```python
y0 = 0
```

**Verification:**
```python
assert sens.shape == (len(t), 1, 1 + 1)
```

### Step 3: Assign t = np.arange.reshape(...)

```python
t = np.arange(0, 12, 0.25).reshape(-1, 1)
```

### Step 4: Assign a = 0.472

```python
a = 0.472
```

### Step 5: Assign y = value

```python
y = 1.0 / (a - 1) * (np.exp(-t) - np.exp(-a * t))
```

### Step 6: Assign ode_model = DifferentialEquation(...)

```python
ode_model = DifferentialEquation(func=ode_func, t0=0, times=t, n_states=1, n_theta=1)
```

### Step 7: Assign unknown = ode_model._simulate(...)

```python
simulated_y, sens = ode_model._simulate([y0], [a])
```

**Verification:**
```python
assert simulated_y.shape == (len(t), 1)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(y, simulated_y, rtol=1e-05)
```


## Complete Example

```python
# Workflow
'Tests the integration in DifferentialEquation'

def ode_func(y, t, p):
    return np.exp(-t) - p[0] * y[0]
y0 = 0
t = np.arange(0, 12, 0.25).reshape(-1, 1)
a = 0.472
y = 1.0 / (a - 1) * (np.exp(-t) - np.exp(-a * t))
ode_model = DifferentialEquation(func=ode_func, t0=0, times=t, n_states=1, n_theta=1)
simulated_y, sens = ode_model._simulate([y0], [a])
assert simulated_y.shape == (len(t), 1)
assert sens.shape == (len(t), 1, 1 + 1)
np.testing.assert_allclose(y, simulated_y, rtol=1e-05)
```

## Next Steps


---

*Source: test_ode.py:29 | Complexity: Advanced | Last updated: 2026-05-18*