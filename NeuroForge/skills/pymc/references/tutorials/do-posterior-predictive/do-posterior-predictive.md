# How To: Do Posterior Predictive

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test do posterior predictive

## Prerequisites

**Required Modules:**
- `arviz`
- `numpy`
- `pytest`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.variational.minibatch_rv`


## Step-by-Step Guide

### Step 1: Assign idata_m = az.from_dict(...)

```python
idata_m = az.from_dict({'posterior': {'x': np.full((2, 500), 25), 'y': np.full((2, 500), np.nan), 'z': np.full((2, 500), np.nan)}})
```

**Verification:**
```python
assert 120 < idata_do.posterior_predictive['z'].mean() < 130
```

### Step 2: Assign m_do = do(...)

```python
m_do = do(m, {y: 100.0})
```

**Verification:**
```python
assert 120 < idata_do.posterior_predictive['z'].mean() < 130
```

### Step 3: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 0, 1)
```

### Step 4: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x, 1)
```

### Step 5: Assign z = pm.Normal(...)

```python
z = pm.Normal('z', y + x, 0.001)
```

### Step 6: Assign idata_do = pm.sample_posterior_predictive(...)

```python
idata_do = pm.sample_posterior_predictive(idata_m, sample_vars=['z'])
```


## Complete Example

```python
# Workflow
with pm.Model() as m:
    x = pm.Normal('x', 0, 1)
    y = pm.Normal('y', x, 1)
    z = pm.Normal('z', y + x, 0.001)
idata_m = az.from_dict({'posterior': {'x': np.full((2, 500), 25), 'y': np.full((2, 500), np.nan), 'z': np.full((2, 500), np.nan)}})
m_do = do(m, {y: 100.0})
with m_do:
    idata_do = pm.sample_posterior_predictive(idata_m, sample_vars=['z'])
assert 120 < idata_do.posterior_predictive['z'].mean() < 130
```

## Next Steps


---

*Source: test_conditioning.py:172 | Complexity: Intermediate | Last updated: 2026-05-18*