# How To: Sample Posterior Predictive After Set Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample posterior predictive after set data

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

### Step 1: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x_test, y_test.posterior_predictive['obs'].mean(('chain', 'draw')), atol=0.1)
```

**Verification:**
```python
assert y_test.posterior_predictive['obs'].shape == (1, 1000, 3)
```

### Step 2: Assign x = pm.Data(...)

```python
x = pm.Data('x', [1.0, 2.0, 3.0])
```

### Step 3: Assign y = pm.Data(...)

```python
y = pm.Data('y', [1.0, 2.0, 3.0])
```

### Step 4: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, 10.0)
```

### Step 5: Call pm.Normal()

```python
pm.Normal('obs', beta * x, np.sqrt(0.01), observed=y)
```

### Step 6: Assign trace = pm.sample(...)

```python
trace = pm.sample(1000, tune=1000, chains=1, return_inferencedata=False, compute_convergence_checks=False)
```

### Step 7: Assign x_test = value

```python
x_test = [5, 6, 9]
```

### Step 8: Call pm.set_data()

```python
pm.set_data(new_data={'x': x_test})
```

### Step 9: Assign y_test = pm.sample_posterior_predictive(...)

```python
y_test = pm.sample_posterior_predictive(trace)
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    x = pm.Data('x', [1.0, 2.0, 3.0])
    y = pm.Data('y', [1.0, 2.0, 3.0])
    beta = pm.Normal('beta', 0, 10.0)
    pm.Normal('obs', beta * x, np.sqrt(0.01), observed=y)
    trace = pm.sample(1000, tune=1000, chains=1, return_inferencedata=False, compute_convergence_checks=False)
with model:
    x_test = [5, 6, 9]
    pm.set_data(new_data={'x': x_test})
    y_test = pm.sample_posterior_predictive(trace)
assert y_test.posterior_predictive['obs'].shape == (1, 1000, 3)
np.testing.assert_allclose(x_test, y_test.posterior_predictive['obs'].mean(('chain', 'draw')), atol=0.1)
```

## Next Steps


---

*Source: test_data.py:74 | Complexity: Advanced | Last updated: 2026-05-18*