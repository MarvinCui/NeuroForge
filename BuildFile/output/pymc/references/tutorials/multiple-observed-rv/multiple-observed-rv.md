# How To: Multiple Observed Rv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test multiple observed rv

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
# Fixtures: log_likelihood
```

## Step-by-Step Guide

### Step 1: Assign y1_data = np.random.randn(...)

```python
y1_data = np.random.randn(10)
```

**Verification:**
```python
assert inference_data.log_likelihood['y1'].shape == (2, 100, 10)
```

### Step 2: Assign y2_data = np.random.randn(...)

```python
y2_data = np.random.randn(100)
```

**Verification:**
```python
assert inference_data.log_likelihood['y1'].shape == (2, 100, 10)
```

### Step 3: Assign test_dict = value

```python
test_dict = {'posterior': ['x'], 'observed_data': ['y1', 'y2'], 'log_likelihood': ['y1', 'y2'], 'sample_stats': ['diverging', '~log_likelihood']}
```

**Verification:**
```python
assert inference_data.log_likelihood['y2'].shape == (2, 100, 100)
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

### Step 6: Call pm.Normal()

```python
pm.Normal('y1', x, 1, observed=y1_data)
```

### Step 7: Call pm.Normal()

```python
pm.Normal('y2', x, 1, observed=y2_data)
```

### Step 8: Call test_dict.pop()

```python
test_dict.pop('log_likelihood')
```

### Step 9: Assign unknown = value

```python
test_dict['~log_likelihood'] = []
```

### Step 10: Assign inference_data = pm.sample(...)

```python
inference_data = pm.sample(100, chains=2, return_inferencedata=True, idata_kwargs={'log_likelihood': log_likelihood})
```

### Step 11: Assign unknown = value

```python
test_dict['log_likelihood'] = ['y1', '~y2']
```

**Verification:**
```python
assert inference_data.log_likelihood['y1'].shape == (2, 100, 10)
```


## Complete Example

```python
# Setup
# Fixtures: log_likelihood

# Workflow
y1_data = np.random.randn(10)
y2_data = np.random.randn(100)
with pm.Model():
    x = pm.Normal('x', 1, 1)
    pm.Normal('y1', x, 1, observed=y1_data)
    pm.Normal('y2', x, 1, observed=y2_data)
    with pytest.warns(FutureWarning, match='Passing `log_likelihood` via `idata_kwargs`'):
        inference_data = pm.sample(100, chains=2, return_inferencedata=True, idata_kwargs={'log_likelihood': log_likelihood})
test_dict = {'posterior': ['x'], 'observed_data': ['y1', 'y2'], 'log_likelihood': ['y1', 'y2'], 'sample_stats': ['diverging', '~log_likelihood']}
if not log_likelihood:
    test_dict.pop('log_likelihood')
    test_dict['~log_likelihood'] = []
elif isinstance(log_likelihood, list):
    test_dict['log_likelihood'] = ['y1', '~y2']
    assert inference_data.log_likelihood['y1'].shape == (2, 100, 10)
else:
    assert inference_data.log_likelihood['y1'].shape == (2, 100, 10)
    assert inference_data.log_likelihood['y2'].shape == (2, 100, 100)
fails = check_multiple_attrs(test_dict, inference_data)
assert not fails
```

## Next Steps


---

*Source: test_arviz.py:397 | Complexity: Advanced | Last updated: 2026-05-18*