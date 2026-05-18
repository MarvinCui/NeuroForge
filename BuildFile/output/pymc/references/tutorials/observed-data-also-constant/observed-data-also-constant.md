# How To: Observed Data Also Constant

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that wen the same variable is used as constant data and observed data, it shows up in both groups.

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
# Fixtures: constant_in_generative_graph
```

## Step-by-Step Guide

### Step 1: 'Test that wen the same variable is used as constant data and observed data, it shows up in both groups.'

```python
'Test that wen the same variable is used as constant data and observed data, it shows up in both groups.'
```

**Verification:**
```python
assert not fails
```

### Step 2: Assign inference_data = to_inference_data(...)

```python
inference_data = to_inference_data(prior=trace, model=model, log_likelihood=False)
```

### Step 3: Assign test_dict = value

```python
test_dict = {'prior': ['sigma'], 'observed_data': ['y']}
```

### Step 4: Assign fails = check_multiple_attrs(...)

```python
fails = check_multiple_attrs(test_dict, inference_data)
```

**Verification:**
```python
assert not fails
```

### Step 5: Assign x = pm.Data(...)

```python
x = pm.Data('x', [1.0, 2.0, 3.0], dims=['trial'])
```

### Step 6: Assign sigma = pm.HalfNormal(...)

```python
sigma = pm.HalfNormal('sigma', 1)
```

### Step 7: Assign mu = value

```python
mu = x - 1 if constant_in_generative_graph else 0
```

### Step 8: Call pm.Normal()

```python
pm.Normal('y', mu, sigma, observed=x, dims=['trial'])
```

### Step 9: Assign trace = pm.sample_prior_predictive(...)

```python
trace = pm.sample_prior_predictive(100, return_inferencedata=False)
```

### Step 10: Assign unknown = value

```python
test_dict['constant_data'] = ['x']
```

### Step 11: Assign unknown = value

```python
test_dict['~constant_data'] = []
```


## Complete Example

```python
# Setup
# Fixtures: constant_in_generative_graph

# Workflow
'Test that wen the same variable is used as constant data and observed data, it shows up in both groups.'
with pm.Model(coords={'trial': [0, 1, 2]}) as model:
    x = pm.Data('x', [1.0, 2.0, 3.0], dims=['trial'])
    sigma = pm.HalfNormal('sigma', 1)
    mu = x - 1 if constant_in_generative_graph else 0
    pm.Normal('y', mu, sigma, observed=x, dims=['trial'])
    trace = pm.sample_prior_predictive(100, return_inferencedata=False)
inference_data = to_inference_data(prior=trace, model=model, log_likelihood=False)
test_dict = {'prior': ['sigma'], 'observed_data': ['y']}
if constant_in_generative_graph:
    test_dict['constant_data'] = ['x']
else:
    test_dict['~constant_data'] = []
fails = check_multiple_attrs(test_dict, inference_data)
assert not fails
```

## Next Steps


---

*Source: test_arviz.py:481 | Complexity: Advanced | Last updated: 2026-05-18*