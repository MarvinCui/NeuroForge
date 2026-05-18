# How To: Missing Data Model

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test missing data model

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign data = ma.masked_values(...)

```python
data = ma.masked_values([1, 2, -1, 4, -1], value=-1)
```

**Verification:**
```python
assert 'y_unobserved' in model.named_vars
```

### Step 2: Assign model = pm.Model(...)

```python
model = pm.Model()
```

**Verification:**
```python
assert not fails
```

### Step 3: Assign test_dict = value

```python
test_dict = {'posterior': ['x', 'y_unobserved'], 'observed_data': ['y_observed'], 'log_likelihood': ['y_observed']}
```

**Verification:**
```python
assert inference_data.log_likelihood['y_observed'].shape == (2, 100, 3)
```

### Step 4: Assign fails = check_multiple_attrs(...)

```python
fails = check_multiple_attrs(test_dict, inference_data)
```

**Verification:**
```python
assert not fails
```

### Step 5: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 1, 1)
```

### Step 6: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x, 1, observed=data)
```

### Step 7: Assign inference_data = pm.sample(...)

```python
inference_data = pm.sample(100, chains=2, return_inferencedata=True, idata_kwargs={'log_likelihood': True})
```


## Complete Example

```python
# Workflow
data = ma.masked_values([1, 2, -1, 4, -1], value=-1)
model = pm.Model()
with model:
    x = pm.Normal('x', 1, 1)
    with pytest.warns(ImputationWarning):
        y = pm.Normal('y', x, 1, observed=data)
    with pytest.warns(FutureWarning, match='Passing `log_likelihood` via `idata_kwargs`'):
        inference_data = pm.sample(100, chains=2, return_inferencedata=True, idata_kwargs={'log_likelihood': True})
assert 'y_unobserved' in model.named_vars
test_dict = {'posterior': ['x', 'y_unobserved'], 'observed_data': ['y_observed'], 'log_likelihood': ['y_observed']}
fails = check_multiple_attrs(test_dict, inference_data)
assert not fails
assert inference_data.log_likelihood['y_observed'].shape == (2, 100, 3)
```

## Next Steps


---

*Source: test_arviz.py:335 | Complexity: Intermediate | Last updated: 2026-05-18*