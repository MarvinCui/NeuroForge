# How To: Scalar Ode 2 Param

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test running model for a scalar ODE with 2 parameters

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

### Step 1: 'Test running model for a scalar ODE with 2 parameters'

```python
'Test running model for a scalar ODE with 2 parameters'
```

**Verification:**
```python
assert idata.posterior['alpha'].shape == (1, 50)
```

### Step 2: Assign times = np.array(...)

```python
times = np.array([0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.5, 4.0, 4.5, 5.0, 5.5, 6.0, 6.5, 7.0, 7.5])
```

**Verification:**
```python
assert idata.posterior['beta'].shape == (1, 50)
```

### Step 3: Assign yobs = value

```python
yobs = np.array([0.31, 0.57, 0.51, 0.55, 0.47, 0.42, 0.38, 0.3, 0.26, 0.22, 0.22, 0.14, 0.14, 0.09, 0.1])[:, np.newaxis]
```

**Verification:**
```python
assert idata.posterior['y0'].shape == (1, 50)
```

### Step 4: Assign ode_model = DifferentialEquation(...)

```python
ode_model = DifferentialEquation(func=system, t0=0, times=times, n_states=1, n_theta=2)
```

**Verification:**
```python
assert idata.posterior['sigma'].shape == (1, 50)
```

### Step 5: Assign alpha = pm.HalfCauchy(...)

```python
alpha = pm.HalfCauchy('alpha', 1)
```

### Step 6: Assign beta = pm.HalfCauchy(...)

```python
beta = pm.HalfCauchy('beta', 1)
```

### Step 7: Assign y0 = pm.LogNormal(...)

```python
y0 = pm.LogNormal('y0', 0, 1)
```

### Step 8: Assign sigma = pm.HalfCauchy(...)

```python
sigma = pm.HalfCauchy('sigma', 1)
```

### Step 9: Assign forward = ode_model(...)

```python
forward = ode_model(theta=[alpha, beta], y0=[y0])
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
idata = pm.sample(50, tune=0, chains=1)
```


## Complete Example

```python
# Workflow
'Test running model for a scalar ODE with 2 parameters'

def system(y, t, p):
    return p[0] * np.exp(-p[0] * t) - p[1] * y[0]
times = np.array([0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.5, 4.0, 4.5, 5.0, 5.5, 6.0, 6.5, 7.0, 7.5])
yobs = np.array([0.31, 0.57, 0.51, 0.55, 0.47, 0.42, 0.38, 0.3, 0.26, 0.22, 0.22, 0.14, 0.14, 0.09, 0.1])[:, np.newaxis]
ode_model = DifferentialEquation(func=system, t0=0, times=times, n_states=1, n_theta=2)
with pm.Model() as model:
    alpha = pm.HalfCauchy('alpha', 1)
    beta = pm.HalfCauchy('beta', 1)
    y0 = pm.LogNormal('y0', 0, 1)
    sigma = pm.HalfCauchy('sigma', 1)
    forward = ode_model(theta=[alpha, beta], y0=[y0])
    y = pm.LogNormal('y', mu=pm.math.log(forward), sigma=sigma, observed=yobs)
    with pytensor.config.change_flags(mode=fast_unstable_sampling_mode):
        with warnings.catch_warnings():
            warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
            warnings.filterwarnings('ignore', 'invalid value encountered in log', RuntimeWarning)
            idata = pm.sample(50, tune=0, chains=1)
assert idata.posterior['alpha'].shape == (1, 50)
assert idata.posterior['beta'].shape == (1, 50)
assert idata.posterior['y0'].shape == (1, 50)
assert idata.posterior['sigma'].shape == (1, 50)
```

## Next Steps


---

*Source: test_ode.py:340 | Complexity: Advanced | Last updated: 2026-05-18*