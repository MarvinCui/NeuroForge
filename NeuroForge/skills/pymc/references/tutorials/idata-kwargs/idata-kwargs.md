# How To: Idata Kwargs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test idata kwargs

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `re`
- `warnings`
- `collections.abc`
- `typing`
- `unittest`
- `jax`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc.exceptions`
- `pymc.sampling.jax`

**Setup Required:**
```python
# Fixtures: model_test_idata_kwargs, sampler, idata_kwargs, postprocessing_backend
```

## Step-by-Step Guide

### Step 1: Assign const_data = idata.get(...)

```python
const_data = idata.get('constant_data')
```

**Verification:**
```python
assert idata is not None
```

### Step 2: Assign posterior = idata.get(...)

```python
posterior = idata.get('posterior')
```

**Verification:**
```python
assert const_data is not None
```

### Step 3: Assign x_dim_expected = value

```python
x_dim_expected = idata_kwargs.get('dims', model_test_idata_kwargs.named_vars_to_dims)['x'][0]
```

**Verification:**
```python
assert 'data' in const_data
```

### Step 4: Assign x_coords_expected = value

```python
x_coords_expected = idata_kwargs.get('coords', model_test_idata_kwargs.coords)[x_dim_expected]
```

**Verification:**
```python
assert 'log_likelihood' in idata
```

### Step 5: Assign idata = sampler(...)

```python
idata = sampler(tune=50, draws=50, chains=1, idata_kwargs=idata_kwargs, postprocessing_backend=postprocessing_backend)
```

**Verification:**
```python
assert 'log_likelihood' not in idata
```


## Complete Example

```python
# Setup
# Fixtures: model_test_idata_kwargs, sampler, idata_kwargs, postprocessing_backend

# Workflow
idata: xr.DataTree | None = None
with model_test_idata_kwargs:
    idata = sampler(tune=50, draws=50, chains=1, idata_kwargs=idata_kwargs, postprocessing_backend=postprocessing_backend)
assert idata is not None
const_data = idata.get('constant_data')
assert const_data is not None
assert 'data' in const_data
if idata_kwargs.get('log_likelihood', False):
    assert 'log_likelihood' in idata
else:
    assert 'log_likelihood' not in idata
posterior = idata.get('posterior')
assert posterior is not None
x_dim_expected = idata_kwargs.get('dims', model_test_idata_kwargs.named_vars_to_dims)['x'][0]
assert x_dim_expected is not None
assert posterior['x'].dims[-1] == x_dim_expected
x_coords_expected = idata_kwargs.get('coords', model_test_idata_kwargs.coords)[x_dim_expected]
assert x_coords_expected is not None
assert list(x_coords_expected) == list(posterior['x'].coords[x_dim_expected].values)
assert posterior['z'].dims[2] == 'z_coord'
assert np.all(posterior['z'].coords['z_coord'].values == np.array(['apple', 'banana', 'orange']))
```

## Next Steps


---

*Source: test_jax.py:267 | Complexity: Intermediate | Last updated: 2026-05-18*