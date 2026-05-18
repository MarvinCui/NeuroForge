# How To: Logp Scalar Ode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the computation of the log probability for these models

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

### Step 1: 'Test the computation of the log probability for these models'

```python
'Test the computation of the log probability for these models'
```

**Verification:**
```python
assert integrated_solution.shape == yobs.shape
```

### Step 2: Assign alpha = 0.4

```python
alpha = 0.4
```

### Step 3: Assign y0 = 0.0

```python
y0 = 0.0
```

### Step 4: Assign times = np.arange(...)

```python
times = np.arange(0.5, 8, 0.5)
```

### Step 5: Assign yobs = value

```python
yobs = np.array([0.3, 0.56, 0.51, 0.55, 0.47, 0.42, 0.38, 0.3, 0.26, 0.21, 0.22, 0.13, 0.13, 0.09, 0.09])[:, np.newaxis]
```

### Step 6: Assign ode_model = DifferentialEquation(...)

```python
ode_model = DifferentialEquation(func=system_1, t0=0, times=times, n_theta=1, n_states=1)
```

### Step 7: Assign unknown = ode_model._simulate(...)

```python
integrated_solution, *_ = ode_model._simulate([y0], [alpha])
```

**Verification:**
```python
assert integrated_solution.shape == yobs.shape
```

### Step 8: Assign manual_logp = norm.logpdf.sum(...)

```python
manual_logp = norm.logpdf(x=np.ravel(yobs), loc=np.ravel(integrated_solution), scale=1).sum()
```

### Step 9: Assign pymc_logp = model_1.compile_logp(...)

```python
pymc_logp = model_1.compile_logp()({})
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(manual_logp, pymc_logp)
```

### Step 11: Assign forward = ode_model(...)

```python
forward = ode_model(theta=[alpha], y0=[y0])
```

### Step 12: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', mu=forward, sigma=1, observed=yobs)
```


## Complete Example

```python
# Workflow
'Test the computation of the log probability for these models'

def system_1(y, t, p):
    return np.exp(-t) - p[0] * y[0]
alpha = 0.4
y0 = 0.0
times = np.arange(0.5, 8, 0.5)
yobs = np.array([0.3, 0.56, 0.51, 0.55, 0.47, 0.42, 0.38, 0.3, 0.26, 0.21, 0.22, 0.13, 0.13, 0.09, 0.09])[:, np.newaxis]
ode_model = DifferentialEquation(func=system_1, t0=0, times=times, n_theta=1, n_states=1)
integrated_solution, *_ = ode_model._simulate([y0], [alpha])
assert integrated_solution.shape == yobs.shape
manual_logp = norm.logpdf(x=np.ravel(yobs), loc=np.ravel(integrated_solution), scale=1).sum()
with pm.Model() as model_1:
    forward = ode_model(theta=[alpha], y0=[y0])
    y = pm.Normal('y', mu=forward, sigma=1, observed=yobs)
pymc_logp = model_1.compile_logp()({})
np.testing.assert_allclose(manual_logp, pymc_logp)
```

## Next Steps


---

*Source: test_ode.py:152 | Complexity: Advanced | Last updated: 2026-05-18*