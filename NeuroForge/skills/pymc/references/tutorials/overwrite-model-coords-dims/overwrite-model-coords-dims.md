# How To: Overwrite Model Coords Dims

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check coords and dims from model object can be partially overwritten.

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

### Step 1: 'Check coords and dims from model object can be partially overwritten.'

```python
'Check coords and dims from model object can be partially overwritten.'
```

**Verification:**
```python
assert not fails1
```

### Step 2: Assign dim1 = value

```python
dim1 = ['a', 'b']
```

**Verification:**
```python
assert not fails2
```

### Step 3: Assign new_dim1 = value

```python
new_dim1 = ['c', 'd']
```

**Verification:**
```python
assert 'dim1' in list(idata1.posterior.beta.dims)
```

### Step 4: Assign coords = value

```python
coords = {'dim1': dim1, 'dim2': ['c1', 'c2']}
```

**Verification:**
```python
assert 'dim2' in list(idata2.posterior.beta.dims)
```

### Step 5: Assign x_data = np.arange.reshape(...)

```python
x_data = np.arange(4).reshape((2, 2))
```

**Verification:**
```python
assert np.all(idata1.constant_data.x.dim1.values == np.array(dim1))
```

### Step 6: Assign y = value

```python
y = x_data + np.random.normal(size=(2, 2))
```

**Verification:**
```python
assert np.all(idata1.constant_data.x.dim2.values == np.array(['c1', 'c2']))
```

### Step 7: Assign test_dict = value

```python
test_dict = {'posterior': ['beta'], 'observed_data': ['obs'], 'constant_data': ['x']}
```

**Verification:**
```python
assert np.all(idata2.constant_data.x.dim1.values == np.array(new_dim1))
```

### Step 8: Assign fails1 = check_multiple_attrs(...)

```python
fails1 = check_multiple_attrs(test_dict, idata1)
```

**Verification:**
```python
assert np.all(idata2.constant_data.x.dim2.values == np.array(['c1', 'c2']))
```

### Step 9: Assign fails2 = check_multiple_attrs(...)

```python
fails2 = check_multiple_attrs(test_dict, idata2)
```

**Verification:**
```python
assert not fails2
```

### Step 10: Assign x = pm.Data(...)

```python
x = pm.Data('x', x_data, dims=('dim1', 'dim2'))
```

### Step 11: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, 1, dims='dim1')
```

### Step 12: Assign _ = pm.Normal(...)

```python
_ = pm.Normal('obs', x * beta, 1, observed=y, dims=('dim1', 'dim2'))
```

### Step 13: Assign idata1 = to_inference_data(...)

```python
idata1 = to_inference_data(trace)
```

### Step 14: Assign idata2 = to_inference_data(...)

```python
idata2 = to_inference_data(trace, coords={'dim1': new_dim1}, dims={'beta': ['dim2']})
```

### Step 15: Assign trace = pm.sample(...)

```python
trace = pm.sample(100, tune=100, return_inferencedata=False)
```


## Complete Example

```python
# Workflow
'Check coords and dims from model object can be partially overwritten.'
dim1 = ['a', 'b']
new_dim1 = ['c', 'd']
coords = {'dim1': dim1, 'dim2': ['c1', 'c2']}
x_data = np.arange(4).reshape((2, 2))
y = x_data + np.random.normal(size=(2, 2))
with pm.Model(coords=coords):
    x = pm.Data('x', x_data, dims=('dim1', 'dim2'))
    beta = pm.Normal('beta', 0, 1, dims='dim1')
    _ = pm.Normal('obs', x * beta, 1, observed=y, dims=('dim1', 'dim2'))
    with pytest.warns(FutureWarning, match='return_inferencedata=False'):
        trace = pm.sample(100, tune=100, return_inferencedata=False)
    idata1 = to_inference_data(trace)
    idata2 = to_inference_data(trace, coords={'dim1': new_dim1}, dims={'beta': ['dim2']})
test_dict = {'posterior': ['beta'], 'observed_data': ['obs'], 'constant_data': ['x']}
fails1 = check_multiple_attrs(test_dict, idata1)
assert not fails1
fails2 = check_multiple_attrs(test_dict, idata2)
assert not fails2
assert 'dim1' in list(idata1.posterior.beta.dims)
assert 'dim2' in list(idata2.posterior.beta.dims)
assert np.all(idata1.constant_data.x.dim1.values == np.array(dim1))
assert np.all(idata1.constant_data.x.dim2.values == np.array(['c1', 'c2']))
assert np.all(idata2.constant_data.x.dim1.values == np.array(new_dim1))
assert np.all(idata2.constant_data.x.dim2.values == np.array(['c1', 'c2']))
```

## Next Steps


---

*Source: test_arviz.py:307 | Complexity: Advanced | Last updated: 2026-05-18*