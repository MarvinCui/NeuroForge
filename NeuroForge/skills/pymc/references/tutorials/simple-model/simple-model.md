# How To: Simple Model

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: simple model

## Prerequisites

**Required Modules:**
- `logging`
- `numpy`
- `pytest`
- `xarray`
- `pymc`
- `pymc.backends`
- `pymc.pytensorf`
- `pymc.step_methods`
- `pymc.step_methods.arraystep`
- `pymc.backends.mcbackend`
- `mcbackend`
- `mcbackend.npproto.utils`


## Step-by-Step Guide

### Step 1: Assign seconds = np.linspace(...)

```python
seconds = np.linspace(0, 5)
```

### Step 2: Assign observations = np.random.normal(...)

```python
observations = np.random.normal(0.5 + np.random.uniform(size=3)[:, None] * seconds[None, :])
```

### Step 3: Assign x = pm.Data(...)

```python
x = pm.Data('seconds', seconds, dims='time')
```

### Step 4: Assign a = pm.Normal(...)

```python
a = pm.Normal('scalar')
```

### Step 5: Assign b = pm.Uniform(...)

```python
b = pm.Uniform('vector', dims='condition')
```

### Step 6: Call pm.Deterministic()

```python
pm.Deterministic('matrix', a + b[:, None] * x[None, :], dims=('condition', 'time'))
```

### Step 7: Call pm.Bernoulli()

```python
pm.Bernoulli('integer', p=0.5)
```

### Step 8: Assign obs = pm.Data(...)

```python
obs = pm.Data('obs', observations, dims=('condition', 'time'))
```

### Step 9: Call pm.Normal()

```python
pm.Normal('L', pmodel['matrix'], observed=obs, dims=('condition', 'time'))
```


## Complete Example

```python
# Workflow
seconds = np.linspace(0, 5)
observations = np.random.normal(0.5 + np.random.uniform(size=3)[:, None] * seconds[None, :])
with pm.Model(coords={'condition': ['A', 'B', 'C']}) as pmodel:
    x = pm.Data('seconds', seconds, dims='time')
    a = pm.Normal('scalar')
    b = pm.Uniform('vector', dims='condition')
    pm.Deterministic('matrix', a + b[:, None] * x[None, :], dims=('condition', 'time'))
    pm.Bernoulli('integer', p=0.5)
    obs = pm.Data('obs', observations, dims=('condition', 'time'))
    pm.Normal('L', pmodel['matrix'], observed=obs, dims=('condition', 'time'))
return pmodel
```

## Next Steps


---

*Source: test_mcbackend.py:43 | Complexity: Advanced | Last updated: 2026-05-18*