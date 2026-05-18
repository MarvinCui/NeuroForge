# How To: Find Map Issue 5923

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test find MAP issue 5923

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytest`
- `numpy.testing`
- `pymc`
- `pymc.exceptions`
- `pymc.step_methods.metropolis`
- `pymc.testing`
- `pymc.tuning`
- `tests`
- `tests.models`


## Step-by-Step Guide

### Step 1: Assign tol = value

```python
tol = 2.0 ** (-11)
```

**Verification:**
```python
assert_allclose(map_est1['mu'], 0, atol=tol)
```

### Step 2: Assign data = np.random.randn(...)

```python
data = np.random.randn(100)
```

**Verification:**
```python
assert_allclose(map_est1['sigma'], 1, atol=tol)
```

### Step 3: Assign data = value

```python
data = (data - np.mean(data)) / np.std(data)
```

**Verification:**
```python
assert_allclose(map_est2['mu'], 0, atol=tol)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(map_est1['mu'], 0, atol=tol)
```

**Verification:**
```python
assert_allclose(map_est2['sigma'], 1, atol=tol)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(map_est1['sigma'], 1, atol=tol)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(map_est2['mu'], 0, atol=tol)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(map_est2['sigma'], 1, atol=tol)
```

### Step 8: Assign mu = pm.Uniform(...)

```python
mu = pm.Uniform('mu', -1, 1)
```

### Step 9: Assign sigma = pm.Uniform(...)

```python
sigma = pm.Uniform('sigma', 0.5, 1.5)
```

### Step 10: Call pm.Normal()

```python
pm.Normal('y', mu=mu, tau=sigma ** (-2), observed=data)
```

### Step 11: Assign start = value

```python
start = {'mu': -0.5, 'sigma': 1.25}
```

### Step 12: Assign map_est1 = find_MAP(...)

```python
map_est1 = find_MAP(progressbar=False, vars=[mu, sigma], start=start)
```

### Step 13: Assign map_est2 = find_MAP(...)

```python
map_est2 = find_MAP(progressbar=False, vars=[sigma, mu], start=start)
```


## Complete Example

```python
# Workflow
tol = 2.0 ** (-11)
data = np.random.randn(100)
data = (data - np.mean(data)) / np.std(data)
with pm.Model():
    mu = pm.Uniform('mu', -1, 1)
    sigma = pm.Uniform('sigma', 0.5, 1.5)
    pm.Normal('y', mu=mu, tau=sigma ** (-2), observed=data)
    start = {'mu': -0.5, 'sigma': 1.25}
    map_est1 = find_MAP(progressbar=False, vars=[mu, sigma], start=start)
    map_est2 = find_MAP(progressbar=False, vars=[sigma, mu], start=start)
assert_allclose(map_est1['mu'], 0, atol=tol)
assert_allclose(map_est1['sigma'], 1, atol=tol)
assert_allclose(map_est2['mu'], 0, atol=tol)
assert_allclose(map_est2['sigma'], 1, atol=tol)
```

## Next Steps


---

*Source: test_starting.py:118 | Complexity: Advanced | Last updated: 2026-05-18*