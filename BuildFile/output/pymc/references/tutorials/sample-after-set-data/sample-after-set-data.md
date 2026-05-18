# How To: Sample After Set Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample after set data

## Prerequisites

**Required Modules:**
- `io`
- `os`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.data`
- `pymc.pytensorf`


## Step-by-Step Guide

### Step 1: Assign new_x = value

```python
new_x = [5.0, 6.0, 9.0]
```

**Verification:**
```python
assert pp_trace.posterior_predictive['obs'].shape == (1, 1000, 3)
```

### Step 2: Assign new_y = value

```python
new_y = [5.0, 6.0, 9.0]
```

**Verification:**
```python
assert pp_trace.posterior_predictive['obs'].shape == (1, 1000, 3)
```

### Step 3: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(new_y, pp_trace.posterior_predictive['obs'].mean(('chain', 'draw')), atol=0.1)
```

### Step 4: Assign x = pm.Data(...)

```python
x = pm.Data('x', [1.0, 2.0, 3.0])
```

### Step 5: Assign y = pm.Data(...)

```python
y = pm.Data('y', [1.0, 2.0, 3.0])
```

### Step 6: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, 10.0)
```

### Step 7: Call pm.Normal()

```python
pm.Normal('obs', beta * x, np.sqrt(0.01), observed=y)
```

### Step 8: Call pm.sample()

```python
pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
```

### Step 9: Call pm.set_data()

```python
pm.set_data(new_data={'x': new_x, 'y': new_y})
```

### Step 10: Assign new_idata = pm.sample(...)

```python
new_idata = pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
```

### Step 11: Assign pp_trace = pm.sample_posterior_predictive(...)

```python
pp_trace = pm.sample_posterior_predictive(new_idata)
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    x = pm.Data('x', [1.0, 2.0, 3.0])
    y = pm.Data('y', [1.0, 2.0, 3.0])
    beta = pm.Normal('beta', 0, 10.0)
    pm.Normal('obs', beta * x, np.sqrt(0.01), observed=y)
    pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
new_x = [5.0, 6.0, 9.0]
new_y = [5.0, 6.0, 9.0]
with model:
    pm.set_data(new_data={'x': new_x, 'y': new_y})
    new_idata = pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
    pp_trace = pm.sample_posterior_predictive(new_idata)
assert pp_trace.posterior_predictive['obs'].shape == (1, 1000, 3)
np.testing.assert_allclose(new_y, pp_trace.posterior_predictive['obs'].mean(('chain', 'draw')), atol=0.1)
```

## Next Steps


---

*Source: test_data.py:123 | Complexity: Advanced | Last updated: 2026-05-18*