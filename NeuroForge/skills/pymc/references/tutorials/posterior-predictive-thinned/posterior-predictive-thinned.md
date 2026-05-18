# How To: Posterior Predictive Thinned

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test posterior predictive thinned

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
# Fixtures: data
```

## Step-by-Step Guide

### Step 1: Assign test_dict = value

```python
test_dict = {'posterior': ['mu', 'tau', 'eta', 'theta'], 'sample_stats': ['diverging', '~log_likelihood'], 'posterior_predictive': ['obs'], 'observed_data': ['obs']}
```

**Verification:**
```python
assert not fails
```

### Step 2: Assign fails = check_multiple_attrs(...)

```python
fails = check_multiple_attrs(test_dict, idata)
```

**Verification:**
```python
assert idata.posterior.sizes['chain'] == 2
```

### Step 3: Assign draws = 20

```python
draws = 20
```

**Verification:**
```python
assert idata.posterior.sizes['draw'] == draws
```

### Step 4: Assign thin_by = 4

```python
thin_by = 4
```

**Verification:**
```python
assert idata.posterior_predictive.sizes['chain'] == 2
```

### Step 5: Assign thinned_idata = idata.sel(...)

```python
thinned_idata = idata.sel(draw=slice(None, None, thin_by))
```

**Verification:**
```python
assert idata.posterior_predictive.sizes['draw'] == draws / thin_by
```

### Step 6: Call idata.update()

```python
idata.update(pm.sample_posterior_predictive(thinned_idata))
```

**Verification:**
```python
assert np.allclose(idata.posterior['draw'], np.arange(draws))
```

### Step 7: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
```

**Verification:**
```python
assert np.allclose(idata.posterior_predictive['draw'], np.arange(draws, step=thin_by))
```

### Step 8: Assign idata = pm.sample(...)

```python
idata = pm.sample(tune=5, draws=draws, chains=2, return_inferencedata=True)
```


## Complete Example

```python
# Setup
# Fixtures: data

# Workflow
with data.model:
    draws = 20
    thin_by = 4
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
        idata = pm.sample(tune=5, draws=draws, chains=2, return_inferencedata=True)
    thinned_idata = idata.sel(draw=slice(None, None, thin_by))
    idata.update(pm.sample_posterior_predictive(thinned_idata))
test_dict = {'posterior': ['mu', 'tau', 'eta', 'theta'], 'sample_stats': ['diverging', '~log_likelihood'], 'posterior_predictive': ['obs'], 'observed_data': ['obs']}
fails = check_multiple_attrs(test_dict, idata)
assert not fails
assert idata.posterior.sizes['chain'] == 2
assert idata.posterior.sizes['draw'] == draws
assert idata.posterior_predictive.sizes['chain'] == 2
assert idata.posterior_predictive.sizes['draw'] == draws / thin_by
assert np.allclose(idata.posterior['draw'], np.arange(draws))
assert np.allclose(idata.posterior_predictive['draw'], np.arange(draws, step=thin_by))
```

## Next Steps


---

*Source: test_arviz.py:232 | Complexity: Advanced | Last updated: 2026-05-18*