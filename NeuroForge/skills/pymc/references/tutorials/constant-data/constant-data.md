# How To: Constant Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test constant_data group behaviour.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytest`
- `xarray`
- `arviz_base.testing`
- `numpy`
- `pytensor.tensor.subtensor`
- `pymc`
- `pymc.backends.arviz`
- `pymc.exceptions`

**Setup Required:**
```python
# Fixtures: use_context
```

## Step-by-Step Guide

### Step 1: 'Test constant_data group behaviour.'

```python
'Test constant_data group behaviour.'
```

**Verification:**
```python
assert not fails
```

### Step 2: Assign test_dict = value

```python
test_dict = {'posterior': ['beta'], 'observed_data': ['obs'], 'constant_data': ['x', 'beta_sigma']}
```

**Verification:**
```python
assert inference_data.log_likelihood['obs'].shape == (2, 100, 3)
```

### Step 3: Assign fails = check_multiple_attrs(...)

```python
fails = check_multiple_attrs(test_dict, inference_data)
```

**Verification:**
```python
assert inference_data.constant_data['beta_sigma'].ndim == 0
```

### Step 4: Assign x = pm.Data(...)

```python
x = pm.Data('x', [1.0, 2.0, 3.0])
```

### Step 5: Assign y = pm.Data(...)

```python
y = pm.Data('y', [1.0, 2.0, 3.0])
```

### Step 6: Assign beta_sigma = pm.Data(...)

```python
beta_sigma = pm.Data('beta_sigma', 1)
```

### Step 7: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, beta_sigma)
```

### Step 8: Assign obs = pm.Normal(...)

```python
obs = pm.Normal('obs', x * beta, 1, observed=y)
```

### Step 9: Assign inference_data = to_inference_data(...)

```python
inference_data = to_inference_data(trace=trace, model=model, log_likelihood=True)
```

### Step 10: Assign trace = pm.sample(...)

```python
trace = pm.sample(100, chains=2, tune=100, return_inferencedata=False)
```

### Step 11: Assign inference_data = to_inference_data(...)

```python
inference_data = to_inference_data(trace=trace, log_likelihood=True)
```


## Complete Example

```python
# Setup
# Fixtures: use_context

# Workflow
'Test constant_data group behaviour.'
with pm.Model() as model:
    x = pm.Data('x', [1.0, 2.0, 3.0])
    y = pm.Data('y', [1.0, 2.0, 3.0])
    beta_sigma = pm.Data('beta_sigma', 1)
    beta = pm.Normal('beta', 0, beta_sigma)
    obs = pm.Normal('obs', x * beta, 1, observed=y)
    with pytest.warns(FutureWarning, match='return_inferencedata=False'):
        trace = pm.sample(100, chains=2, tune=100, return_inferencedata=False)
    if use_context:
        inference_data = to_inference_data(trace=trace, log_likelihood=True)
if not use_context:
    inference_data = to_inference_data(trace=trace, model=model, log_likelihood=True)
test_dict = {'posterior': ['beta'], 'observed_data': ['obs'], 'constant_data': ['x', 'beta_sigma']}
fails = check_multiple_attrs(test_dict, inference_data)
assert not fails
assert inference_data.log_likelihood['obs'].shape == (2, 100, 3)
assert inference_data.constant_data['beta_sigma'].ndim == 0
```

## Next Steps


---

*Source: test_arviz.py:454 | Complexity: Advanced | Last updated: 2026-05-18*