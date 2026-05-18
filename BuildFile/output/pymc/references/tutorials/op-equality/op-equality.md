# How To: Op Equality

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests that the equality of mathematically identical Ops evaluates True

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

### Step 1: 'Tests that the equality of mathematically identical Ops evaluates True'

```python
'Tests that the equality of mathematically identical Ops evaluates True'
```

**Verification:**
```python
assert op_1 == op_2
```

### Step 2: Assign t = np.linspace(...)

```python
t = np.linspace(0, 2, 12)
```

**Verification:**
```python
assert op_1 != op_other
```

### Step 3: Assign op_1 = DifferentialEquation(...)

```python
op_1 = DifferentialEquation(func=ode_func, t0=0, times=t, n_states=1, n_theta=1)
```

### Step 4: Assign op_2 = DifferentialEquation(...)

```python
op_2 = DifferentialEquation(func=ode_func, t0=0, times=t, n_states=1, n_theta=1)
```

### Step 5: Assign op_other = DifferentialEquation(...)

```python
op_other = DifferentialEquation(func=ode_func, t0=0, times=np.linspace(0, 2, 16), n_states=1, n_theta=1)
```

**Verification:**
```python
assert op_1 == op_2
```


## Complete Example

```python
# Workflow
'Tests that the equality of mathematically identical Ops evaluates True'

def ode_func(y, t, p):
    return np.exp(-t) - p[0] * y[0]
t = np.linspace(0, 2, 12)
op_1 = DifferentialEquation(func=ode_func, t0=0, times=t, n_states=1, n_theta=1)
op_2 = DifferentialEquation(func=ode_func, t0=0, times=t, n_states=1, n_theta=1)
op_other = DifferentialEquation(func=ode_func, t0=0, times=np.linspace(0, 2, 16), n_states=1, n_theta=1)
assert op_1 == op_2
assert op_1 != op_other
return
```

## Next Steps


---

*Source: test_ode.py:285 | Complexity: Intermediate | Last updated: 2026-05-18*