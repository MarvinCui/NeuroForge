# How To: Gradients

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests the computation of the sensitivities from the PyTensor computation graph

## Prerequisites

**Required Modules:**
- `numpy`
- `scipy.integrate`
- `pymc.ode.utils`


## Step-by-Step Guide

### Step 1: 'Tests the computation of the sensitivities from the PyTensor computation graph'

```python
'Tests the computation of the sensitivities from the PyTensor computation graph'
```

### Step 2: Assign augmented_ode_func = augment_system(...)

```python
augmented_ode_func = augment_system(ode_func, n_states=1, n_theta=1)
```

### Step 3: Assign y0 = 0.0

```python
y0 = 0.0
```

### Step 4: Assign t = np.arange.reshape(...)

```python
t = np.arange(0, 12, 0.25).reshape(-1, 1)
```

### Step 5: Assign a = 0.472

```python
a = 0.472
```

### Step 6: Assign p = np.array(...)

```python
p = np.array([y0, a])
```

### Step 7: Assign y0_sensitivity = np.exp(...)

```python
y0_sensitivity = np.exp(-a * t)
```

### Step 8: Assign a_sensitivity = value

```python
a_sensitivity = -(np.exp(t * (a - 1)) - 1 + (a - 1) * (y0 * a - y0 - 1) * t) * np.exp(-a * t) / (a - 1) ** 2
```

### Step 9: Assign sensitivity = value

```python
sensitivity = np.c_[y0_sensitivity, a_sensitivity]
```

### Step 10: Assign integrated_solutions = ode.odeint(...)

```python
integrated_solutions = ode.odeint(func=augmented_system, y0=[y0, 1, 0], t=t.ravel(), args=(p,))
```

### Step 11: Assign simulated_sensitivity = value

```python
simulated_sensitivity = integrated_solutions[:, 1:]
```

### Step 12: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(sensitivity, simulated_sensitivity, rtol=1e-05)
```

### Step 13: Assign unknown = augmented_ode_func(...)

```python
dydt, ddt_dydp = augmented_ode_func(Y[:1], t, p, Y[1:])
```

### Step 14: Assign derivatives = np.concatenate(...)

```python
derivatives = np.concatenate([dydt, ddt_dydp])
```


## Complete Example

```python
# Workflow
'Tests the computation of the sensitivities from the PyTensor computation graph'

def ode_func(y, t, p):
    return np.exp(-t) - p[0] * y[0]
augmented_ode_func = augment_system(ode_func, n_states=1, n_theta=1)

def augmented_system(Y, t, p):
    dydt, ddt_dydp = augmented_ode_func(Y[:1], t, p, Y[1:])
    derivatives = np.concatenate([dydt, ddt_dydp])
    return derivatives
y0 = 0.0
t = np.arange(0, 12, 0.25).reshape(-1, 1)
a = 0.472
p = np.array([y0, a])
y0_sensitivity = np.exp(-a * t)
a_sensitivity = -(np.exp(t * (a - 1)) - 1 + (a - 1) * (y0 * a - y0 - 1) * t) * np.exp(-a * t) / (a - 1) ** 2
sensitivity = np.c_[y0_sensitivity, a_sensitivity]
integrated_solutions = ode.odeint(func=augmented_system, y0=[y0, 1, 0], t=t.ravel(), args=(p,))
simulated_sensitivity = integrated_solutions[:, 1:]
np.testing.assert_allclose(sensitivity, simulated_sensitivity, rtol=1e-05)
```

## Next Steps


---

*Source: test_utils.py:21 | Complexity: Advanced | Last updated: 2026-05-18*