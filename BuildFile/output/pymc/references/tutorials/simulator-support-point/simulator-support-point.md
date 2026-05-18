# How To: Simulator Support Point

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test simulator support point

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.link.numba`
- `pytensor.tensor.random.op`
- `pytensor.tensor.random.variable`
- `pytensor.tensor.sort`
- `pymc`
- `pymc.initial_point`
- `pymc.pytensorf`
- `pymc.smc.kernels`

**Setup Required:**
```python
# Fixtures: seeded_test, mu, sigma, size
```

## Step-by-Step Guide

### Step 1: Assign fn = make_initial_point_fn(...)

```python
fn = make_initial_point_fn(model=model, return_transformed=False, default_strategy='support_point')
```

**Verification:**
```python
assert result.shape == random_draw.shape
```

### Step 2: Assign random_draw = unknown.eval(...)

```python
random_draw = model['x'].eval()
```

**Verification:**
```python
assert np.all(np.abs((result - expected_sample_mean) / expected_sample_mean_std) < cutoff)
```

### Step 3: Assign result = value

```python
result = fn(0)['x']
```

**Verification:**
```python
assert result.shape == random_draw.shape
```

### Step 4: Assign n = 10

```python
n = 10
```

### Step 5: Assign expected_sample_mean = mu

```python
expected_sample_mean = mu
```

### Step 6: Assign expected_sample_mean_std = np.sqrt(...)

```python
expected_sample_mean_std = np.sqrt(sigma ** 2 / n)
```

### Step 7: Assign alpha = 0.01

```python
alpha = 0.01
```

### Step 8: Assign cutoff = st.norm.ppf(...)

```python
cutoff = st.norm().ppf(1 - alpha / 2)
```

**Verification:**
```python
assert np.all(np.abs((result - expected_sample_mean) / expected_sample_mean_std) < cutoff)
```

### Step 9: Assign x = pm.Simulator(...)

```python
x = pm.Simulator('x', normal_sim, mu, sigma, size=size)
```


## Complete Example

```python
# Setup
# Fixtures: seeded_test, mu, sigma, size

# Workflow
def normal_sim(rng, mu, sigma, size):
    return rng.normal(mu, sigma, size=size)
with pm.Model() as model:
    x = pm.Simulator('x', normal_sim, mu, sigma, size=size)
fn = make_initial_point_fn(model=model, return_transformed=False, default_strategy='support_point')
random_draw = model['x'].eval()
result = fn(0)['x']
assert result.shape == random_draw.shape
n = 10
expected_sample_mean = mu
expected_sample_mean_std = np.sqrt(sigma ** 2 / n)
alpha = 0.01
alpha /= 2 * 2 * 3
alpha /= random_draw.size
cutoff = st.norm().ppf(1 - alpha / 2)
assert np.all(np.abs((result - expected_sample_mean) / expected_sample_mean_std) < cutoff)
```

## Next Steps


---

*Source: test_simulator.py:336 | Complexity: Advanced | Last updated: 2026-05-18*