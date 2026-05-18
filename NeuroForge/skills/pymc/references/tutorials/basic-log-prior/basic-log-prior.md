# How To: Basic Log Prior

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test basic log prior

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `unittest.mock`
- `numpy`
- `pytest`
- `scipy.stats`
- `arviz_base`
- `pytensor.compile`
- `pymc.distributions`
- `pymc.distributions.transforms`
- `pymc.model`
- `pymc.stats.log_density`
- `tests.distributions.test_multivariate`

**Setup Required:**
```python
# Fixtures: transform
```

## Step-by-Step Guide

### Step 1: Assign transform = value

```python
transform = log if transform else None
```

**Verification:**
```python
assert m.rvs_to_values[x] is x_value_var
```

### Step 2: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(res.log_prior['x'].values, st.norm(0, 1).logpdf(idata.posterior['x'].values))
```

**Verification:**
```python
assert m.rvs_to_transforms[x] is transform
```

### Step 3: Assign x = Normal(...)

```python
x = Normal('x', transform=transform)
```

**Verification:**
```python
assert res is idata
```

### Step 4: Assign x_value_var = value

```python
x_value_var = m.rvs_to_values[x]
```

**Verification:**
```python
assert res.log_prior.sizes == {'chain': 4, 'draw': 25}
```

### Step 5: Call Normal()

```python
Normal('y', x, observed=[0, 1, 2])
```

### Step 6: Assign idata = from_dict(...)

```python
idata = from_dict({'posterior': {'x': np.arange(100).reshape(4, 25)}})
```

### Step 7: Assign res = compute_log_prior(...)

```python
res = compute_log_prior(idata)
```


## Complete Example

```python
# Setup
# Fixtures: transform

# Workflow
transform = log if transform else None
with Model() as m:
    x = Normal('x', transform=transform)
    x_value_var = m.rvs_to_values[x]
    Normal('y', x, observed=[0, 1, 2])
    idata = from_dict({'posterior': {'x': np.arange(100).reshape(4, 25)}})
    res = compute_log_prior(idata)
assert m.rvs_to_values[x] is x_value_var
assert m.rvs_to_transforms[x] is transform
assert res is idata
assert res.log_prior.sizes == {'chain': 4, 'draw': 25}
np.testing.assert_allclose(res.log_prior['x'].values, st.norm(0, 1).logpdf(idata.posterior['x'].values))
```

## Next Steps


---

*Source: test_log_density.py:140 | Complexity: Intermediate | Last updated: 2026-05-18*