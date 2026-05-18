# How To: Autodetect Coords From Model

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test autodetect coords from model

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

### Step 1: Assign pd = pytest.importorskip(...)

```python
pd = pytest.importorskip('pandas')
```

**Verification:**
```python
assert 'city' in list(idata.posterior.dims)
```

### Step 2: Assign df_data = pd.DataFrame.set_index(...)

```python
df_data = pd.DataFrame(columns=['date']).set_index('date')
```

**Verification:**
```python
assert 'city' in list(idata.observed_data.dims)
```

### Step 3: Assign dates = pd.date_range(...)

```python
dates = pd.date_range(start='2020-05-01', end='2020-05-20')
```

**Verification:**
```python
assert 'date' in list(idata.observed_data.dims)
```

### Step 4: Assign df_data.index = dates

```python
df_data.index = dates
```

### Step 5: Assign df_data.index.name = 'date'

```python
df_data.index.name = 'date'
```

### Step 6: Assign coords = value

```python
coords = {'date': df_data.index, 'city': df_data.columns}
```

**Verification:**
```python
assert 'city' in list(idata.posterior.dims)
```

### Step 7: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(idata.posterior.coords['city'], coords['city'])
```

### Step 8: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(idata.observed_data.coords['date'], coords['date'])
```

### Step 9: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(idata.observed_data.coords['city'], coords['city'])
```

### Step 10: Assign unknown = np.random.normal(...)

```python
df_data[city] = np.random.normal(loc=mu, size=len(dates))
```

### Step 11: Assign europe_mean = pm.Normal(...)

```python
europe_mean = pm.Normal('europe_mean_temp', mu=15.0, sigma=3.0)
```

### Step 12: Assign city_offset = pm.Normal(...)

```python
city_offset = pm.Normal('city_offset', mu=0.0, sigma=3.0, dims='city')
```

### Step 13: Assign city_temperature = pm.Deterministic(...)

```python
city_temperature = pm.Deterministic('city_temperature', europe_mean + city_offset, dims='city')
```

### Step 14: Assign data_dims = value

```python
data_dims = ('date', 'city')
```

### Step 15: Assign data = pm.Data(...)

```python
data = pm.Data('data', df_data, dims=data_dims)
```

### Step 16: Assign _ = pm.Normal(...)

```python
_ = pm.Normal('likelihood', mu=city_temperature, sigma=0.5, observed=data, dims=data_dims)
```

### Step 17: Assign trace = pm.sample(...)

```python
trace = pm.sample(return_inferencedata=False, compute_convergence_checks=False, cores=1, chains=1, tune=20, draws=30, step=pm.Metropolis())
```

### Step 18: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
```

### Step 19: Assign idata = to_inference_data(...)

```python
idata = to_inference_data(trace=trace, model=model)
```

### Step 20: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
```

### Step 21: Assign idata = to_inference_data(...)

```python
idata = to_inference_data(trace=trace)
```


## Complete Example

```python
# Setup
# Fixtures: use_context

# Workflow
pd = pytest.importorskip('pandas')
df_data = pd.DataFrame(columns=['date']).set_index('date')
dates = pd.date_range(start='2020-05-01', end='2020-05-20')
for city, mu in {'Berlin': 15, 'San Marino': 18, 'Paris': 16}.items():
    df_data[city] = np.random.normal(loc=mu, size=len(dates))
df_data.index = dates
df_data.index.name = 'date'
coords = {'date': df_data.index, 'city': df_data.columns}
with pm.Model(coords=coords) as model:
    europe_mean = pm.Normal('europe_mean_temp', mu=15.0, sigma=3.0)
    city_offset = pm.Normal('city_offset', mu=0.0, sigma=3.0, dims='city')
    city_temperature = pm.Deterministic('city_temperature', europe_mean + city_offset, dims='city')
    data_dims = ('date', 'city')
    data = pm.Data('data', df_data, dims=data_dims)
    _ = pm.Normal('likelihood', mu=city_temperature, sigma=0.5, observed=data, dims=data_dims)
    with pytest.warns(FutureWarning, match='return_inferencedata=False'):
        trace = pm.sample(return_inferencedata=False, compute_convergence_checks=False, cores=1, chains=1, tune=20, draws=30, step=pm.Metropolis())
    if use_context:
        with warnings.catch_warnings():
            warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
            idata = to_inference_data(trace=trace)
if not use_context:
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
        idata = to_inference_data(trace=trace, model=model)
assert 'city' in list(idata.posterior.dims)
assert 'city' in list(idata.observed_data.dims)
assert 'date' in list(idata.observed_data.dims)
np.testing.assert_array_equal(idata.posterior.coords['city'], coords['city'])
np.testing.assert_array_equal(idata.observed_data.coords['date'], coords['date'])
np.testing.assert_array_equal(idata.observed_data.coords['city'], coords['city'])
```

## Next Steps


---

*Source: test_arviz.py:257 | Complexity: Advanced | Last updated: 2026-05-18*