# How To: Scaling Data Works In Likelihood

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test scaling data works in likelihood

## Prerequisites

**Required Modules:**
- `io`
- `os`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.data`
- `pymc.pytensorf`


## Step-by-Step Guide

### Step 1: Assign data = np.array(...)

```python
data = np.array([10, 11, 12, 13, 14, 15])
```

### Step 2: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(idata.observed_data['x'].values, data / scale)
```

### Step 3: Assign target = pm.Data(...)

```python
target = pm.Data('target', data)
```

### Step 4: Assign scale = 12

```python
scale = 12
```

### Step 5: Assign scaled_target = value

```python
scaled_target = target / scale
```

### Step 6: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', mu=0, sigma=1)
```

### Step 7: Call pm.Normal()

```python
pm.Normal('x', mu=mu, sigma=1, observed=scaled_target)
```

### Step 8: Assign idata = pm.sample(...)

```python
idata = pm.sample(10, chains=1, tune=100)
```


## Complete Example

```python
# Workflow
data = np.array([10, 11, 12, 13, 14, 15])
with pm.Model():
    target = pm.Data('target', data)
    scale = 12
    scaled_target = target / scale
    mu = pm.Normal('mu', mu=0, sigma=1)
    pm.Normal('x', mu=mu, sigma=1, observed=scaled_target)
    idata = pm.sample(10, chains=1, tune=100)
np.testing.assert_allclose(idata.observed_data['x'].values, data / scale)
```

## Next Steps


---

*Source: test_data.py:541 | Complexity: Advanced | Last updated: 2026-05-18*