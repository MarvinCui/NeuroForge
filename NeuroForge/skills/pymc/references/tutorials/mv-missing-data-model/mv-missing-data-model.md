# How To: Mv Missing Data Model

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mv missing data model

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
data = ma.masked_values([[1, 2], [2, 2], [-1, 4], [2, -1], [-1, -1]], value=-1)
```

**Verification:**
```python
assert isinstance(y.owner.inputs[0].owner.op, AdvancedIncSubtensor | AdvancedIncSubtensor1)
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
test_dict = {'posterior': ['mu', 'chol_cov'], 'observed_data': ['y_observed'], 'log_likelihood': ['y_observed']}
```

### Step 4: Assign fails = check_multiple_attrs(...)

```python
fails = check_multiple_attrs(test_dict, inference_data)
```

**Verification:**
```python
assert not fails
```

### Step 5: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', 0, 1, size=2)
```

### Step 6: Assign sd_dist = pm.HalfNormal.dist(...)

```python
sd_dist = pm.HalfNormal.dist(1.0, size=2)
```

### Step 7: Assign unknown = pm.LKJCholeskyCov(...)

```python
chol, *_ = pm.LKJCholeskyCov('chol_cov', n=2, eta=1, sd_dist=sd_dist)
```

### Step 8: Assign y = pm.MvNormal(...)

```python
y = pm.MvNormal('y', mu=mu, chol=chol, observed=data)
```

### Step 9: Assign inference_data = pm.sample(...)

```python
inference_data = pm.sample(tune=10, draws=10, chains=2, step=pm.Metropolis(), idata_kwargs={'log_likelihood': True})
```


## Complete Example

```python
# Workflow
data = ma.masked_values([[1, 2], [2, 2], [-1, 4], [2, -1], [-1, -1]], value=-1)
model = pm.Model()
with model:
    mu = pm.Normal('mu', 0, 1, size=2)
    sd_dist = pm.HalfNormal.dist(1.0, size=2)
    chol, *_ = pm.LKJCholeskyCov('chol_cov', n=2, eta=1, sd_dist=sd_dist)
    with pytest.warns(ImputationWarning):
        y = pm.MvNormal('y', mu=mu, chol=chol, observed=data)
    with pytest.warns(FutureWarning, match='Passing `log_likelihood` via `idata_kwargs`'):
        inference_data = pm.sample(tune=10, draws=10, chains=2, step=pm.Metropolis(), idata_kwargs={'log_likelihood': True})
assert isinstance(y.owner.inputs[0].owner.op, AdvancedIncSubtensor | AdvancedIncSubtensor1)
test_dict = {'posterior': ['mu', 'chol_cov'], 'observed_data': ['y_observed'], 'log_likelihood': ['y_observed']}
fails = check_multiple_attrs(test_dict, inference_data)
assert not fails
```

## Next Steps


---

*Source: test_arviz.py:366 | Complexity: Advanced | Last updated: 2026-05-18*