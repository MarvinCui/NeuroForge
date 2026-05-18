# How To: Censored Invalid Dist

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test censored invalid dist

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `scipy`
- `pymc`
- `pymc`
- `pymc.distributions.shape_utils`


## Step-by-Step Guide

### Step 1: Assign invalid_dist = value

```python
invalid_dist = pm.Normal
```

### Step 2: Assign mv_dist = pm.Dirichlet.dist(...)

```python
mv_dist = pm.Dirichlet.dist(a=[1, 1, 1])
```

### Step 3: Assign registered_dist = pm.Normal(...)

```python
registered_dist = pm.Normal('dist')
```

### Step 4: Assign x = pm.Censored(...)

```python
x = pm.Censored('x', invalid_dist, lower=None, upper=None)
```

### Step 5: Assign x = pm.Censored(...)

```python
x = pm.Censored('x', mv_dist, lower=None, upper=None)
```

### Step 6: Assign x = pm.Censored(...)

```python
x = pm.Censored('x', registered_dist, lower=None, upper=None)
```


## Complete Example

```python
# Workflow
with pm.Model():
    invalid_dist = pm.Normal
    with pytest.raises(ValueError, match='Censoring dist must be a distribution created via the'):
        x = pm.Censored('x', invalid_dist, lower=None, upper=None)
with pm.Model():
    mv_dist = pm.Dirichlet.dist(a=[1, 1, 1])
    with pytest.raises(NotImplementedError, match='Censoring of multivariate distributions has not been implemented yet'):
        x = pm.Censored('x', mv_dist, lower=None, upper=None)
with pm.Model():
    registered_dist = pm.Normal('dist')
    with pytest.raises(ValueError, match='The dist dist was already registered in the current model'):
        x = pm.Censored('x', registered_dist, lower=None, upper=None)
```

## Next Steps


---

*Source: test_censored.py:70 | Complexity: Intermediate | Last updated: 2026-05-18*