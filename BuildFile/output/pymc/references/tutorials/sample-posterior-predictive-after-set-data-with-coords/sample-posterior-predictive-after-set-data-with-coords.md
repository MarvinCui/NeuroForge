# How To: Sample Posterior Predictive After Set Data With Coords

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample posterior predictive after set data with coords

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

### Step 1: Assign y = np.array(...)

```python
y = np.array([1.0, 2.0, 3.0])
```

**Verification:**
```python
assert idata.predictions['obs'].shape == (1, 10, 2)
```

### Step 2: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x_test, idata.predictions['obs'].mean(('chain', 'draw')), atol=0.1)
```

**Verification:**
```python
assert np.all(idata.predictions['obs_id'].values == np.array(['a', 'b']))
```

### Step 3: Assign x = pm.Data(...)

```python
x = pm.Data('x', [1.0, 2.0, 3.0], dims='obs_id')
```

### Step 4: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, 10.0)
```

### Step 5: Call pm.Normal()

```python
pm.Normal('obs', beta * x, np.sqrt(0.001), observed=y, dims='obs_id')
```

### Step 6: Assign idata = pm.sample(...)

```python
idata = pm.sample(10, tune=100, chains=1, return_inferencedata=True, compute_convergence_checks=False)
```

### Step 7: Assign x_test = value

```python
x_test = [5, 6]
```

### Step 8: Call pm.set_data()

```python
pm.set_data(new_data={'x': x_test}, coords={'obs_id': ['a', 'b']})
```

### Step 9: Call pm.sample_posterior_predictive()

```python
pm.sample_posterior_predictive(idata, extend_inferencedata=True, predictions=True)
```


## Complete Example

```python
# Workflow
y = np.array([1.0, 2.0, 3.0])
with pm.Model() as model:
    x = pm.Data('x', [1.0, 2.0, 3.0], dims='obs_id')
    beta = pm.Normal('beta', 0, 10.0)
    pm.Normal('obs', beta * x, np.sqrt(0.001), observed=y, dims='obs_id')
    idata = pm.sample(10, tune=100, chains=1, return_inferencedata=True, compute_convergence_checks=False)
with model:
    x_test = [5, 6]
    pm.set_data(new_data={'x': x_test}, coords={'obs_id': ['a', 'b']})
    pm.sample_posterior_predictive(idata, extend_inferencedata=True, predictions=True)
assert idata.predictions['obs'].shape == (1, 10, 2)
assert np.all(idata.predictions['obs_id'].values == np.array(['a', 'b']))
np.testing.assert_allclose(x_test, idata.predictions['obs'].mean(('chain', 'draw')), atol=0.1)
```

## Next Steps


---

*Source: test_data.py:98 | Complexity: Advanced | Last updated: 2026-05-18*