# How To: Parametrization

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test parametrization

## Prerequisites

**Required Modules:**
- `arviz`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.spatial`
- `pymc`


## Step-by-Step Guide

### Step 1: Assign err_msg = '`m` must be a positive integer as the `Periodic` kernel approximation is only implemented for 1-dimensional case.'

```python
err_msg = '`m` must be a positive integer as the `Periodic` kernel approximation is only implemented for 1-dimensional case.'
```

### Step 2: Assign cov_func = pm.gp.cov.Periodic(...)

```python
cov_func = pm.gp.cov.Periodic(1, period=1, ls=0.1)
```

### Step 3: Call pm.gp.HSGPPeriodic()

```python
pm.gp.HSGPPeriodic(m=[500], cov_func=cov_func)
```

### Step 4: Assign cov_func = pm.gp.cov.Periodic(...)

```python
cov_func = pm.gp.cov.Periodic(1, period=1, ls=0.1)
```

### Step 5: Call pm.gp.HSGPPeriodic()

```python
pm.gp.HSGPPeriodic(m=-1, cov_func=cov_func)
```

### Step 6: Assign cov_func = value

```python
cov_func = 5.0 * pm.gp.cov.Periodic(1, period=1, ls=0.1)
```

### Step 7: Call pm.gp.HSGPPeriodic()

```python
pm.gp.HSGPPeriodic(m=500, cov_func=cov_func)
```

### Step 8: Assign cov_func = pm.gp.cov.Periodic(...)

```python
cov_func = pm.gp.cov.Periodic(2, period=1, ls=[1, 2])
```

### Step 9: Call pm.gp.HSGPPeriodic()

```python
pm.gp.HSGPPeriodic(m=500, scale=0.5, cov_func=cov_func)
```


## Complete Example

```python
# Workflow
err_msg = '`m` must be a positive integer as the `Periodic` kernel approximation is only implemented for 1-dimensional case.'
with pytest.raises(ValueError, match=err_msg):
    cov_func = pm.gp.cov.Periodic(1, period=1, ls=0.1)
    pm.gp.HSGPPeriodic(m=[500], cov_func=cov_func)
with pytest.raises(ValueError, match=err_msg):
    cov_func = pm.gp.cov.Periodic(1, period=1, ls=0.1)
    pm.gp.HSGPPeriodic(m=-1, cov_func=cov_func)
with pytest.raises(ValueError, match='`cov_func` must be an instance of a `Periodic` kernel only. Use the `scale` parameter to control the variance.'):
    cov_func = 5.0 * pm.gp.cov.Periodic(1, period=1, ls=0.1)
    pm.gp.HSGPPeriodic(m=500, cov_func=cov_func)
with pytest.raises(ValueError, match='HSGP approximation for `Periodic` kernel only implemented for 1-dimensional case.'):
    cov_func = pm.gp.cov.Periodic(2, period=1, ls=[1, 2])
    pm.gp.HSGPPeriodic(m=500, scale=0.5, cov_func=cov_func)
```

## Next Steps


---

*Source: test_hsgp_approx.py:255 | Complexity: Advanced | Last updated: 2026-05-18*