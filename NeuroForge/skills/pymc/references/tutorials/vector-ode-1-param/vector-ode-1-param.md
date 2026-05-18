# How To: Vector Ode 1 Param

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test running model for a vector ODE with 1 parameter

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

### Step 1: 'Test running model for a vector ODE with 1 parameter'

```python
'Test running model for a vector ODE with 1 parameter'
```

**Verification:**
```python
assert idata.posterior['R'].shape == (1, 50)
```

### Step 2: Assign times = np.array(...)

```python
times = np.array([0.0, 0.8, 1.6, 2.4, 3.2, 4.0, 4.8, 5.6, 6.4, 7.2, 8.0])
```

**Verification:**
```python
assert idata.posterior['sigma'].shape == (1, 50, 2)
```

### Step 3: Assign yobs = np.array(...)

```python
yobs = np.array([[1.02, 0.02], [0.86, 0.12], [0.43, 0.37], [0.14, 0.42], [0.05, 0.43], [0.03, 0.14], [0.02, 0.08], [0.02, 0.04], [0.02, 0.01], [0.02, 0.01], [0.02, 0.01]])
```

### Step 4: Assign ode_model = DifferentialEquation(...)

```python
ode_model = DifferentialEquation(func=system, t0=0, times=times, n_states=2, n_theta=1)
```

**Verification:**
```python
assert idata.posterior['R'].shape == (1, 50)
```

### Step 5: Assign ds = value

```python
ds = -p[0] * y[0] * y[1]
```

### Step 6: Assign di = value

```python
di = p[0] * y[0] * y[1] - y[1]
```

### Step 7: Assign R = pm.LogNormal(...)

```python
R = pm.LogNormal('R', 1, 5, initval=1)
```

### Step 8: Assign sigma = pm.HalfCauchy(...)

```python
sigma = pm.HalfCauchy('sigma', 1, shape=2, initval=[0.5, 0.5])
```

### Step 9: Assign forward = ode_model(...)

```python
forward = ode_model(theta=[R], y0=[0.99, 0.01])
```

### Step 10: Assign y = pm.LogNormal(...)

```python
y = pm.LogNormal('y', mu=pm.math.log(forward), sigma=sigma, observed=yobs)
```

### Step 11: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
```

### Step 12: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'invalid value encountered in log', RuntimeWarning)
```

### Step 13: Assign idata = pm.sample(...)

```python
idata = pm.sample(50, tune=0, chains=1, progressbar=False, compute_convergence_checks=False)
```


## Complete Example

```python
# Workflow
'Test running model for a vector ODE with 1 parameter'

def system(y, t, p):
    ds = -p[0] * y[0] * y[1]
    di = p[0] * y[0] * y[1] - y[1]
    return [ds, di]
times = np.array([0.0, 0.8, 1.6, 2.4, 3.2, 4.0, 4.8, 5.6, 6.4, 7.2, 8.0])
yobs = np.array([[1.02, 0.02], [0.86, 0.12], [0.43, 0.37], [0.14, 0.42], [0.05, 0.43], [0.03, 0.14], [0.02, 0.08], [0.02, 0.04], [0.02, 0.01], [0.02, 0.01], [0.02, 0.01]])
ode_model = DifferentialEquation(func=system, t0=0, times=times, n_states=2, n_theta=1)
with pm.Model() as model:
    R = pm.LogNormal('R', 1, 5, initval=1)
    sigma = pm.HalfCauchy('sigma', 1, shape=2, initval=[0.5, 0.5])
    forward = ode_model(theta=[R], y0=[0.99, 0.01])
    y = pm.LogNormal('y', mu=pm.math.log(forward), sigma=sigma, observed=yobs)
    with pytensor.config.change_flags(mode=fast_unstable_sampling_mode):
        with warnings.catch_warnings():
            warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
            warnings.filterwarnings('ignore', 'invalid value encountered in log', RuntimeWarning)
            idata = pm.sample(50, tune=0, chains=1, progressbar=False, compute_convergence_checks=False)
assert idata.posterior['R'].shape == (1, 50)
assert idata.posterior['sigma'].shape == (1, 50, 2)
```

## Next Steps


---

*Source: test_ode.py:377 | Complexity: Advanced | Last updated: 2026-05-18*