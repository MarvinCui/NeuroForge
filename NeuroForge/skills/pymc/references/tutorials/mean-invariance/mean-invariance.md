# How To: Mean Invariance

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mean invariance

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

### Step 1: Assign X = value

```python
X = np.linspace(0, 10, 100)[:, None]
```

**Verification:**
```python
assert np.allclose(gp._X_center, original_center), 'gp._X_center should not change after updating data for out-of-sample predictions.'
```

### Step 2: Assign original_center = value

```python
original_center = (np.max(X, axis=0) - np.min(X, axis=0)) / 2
```

### Step 3: Assign x_new = value

```python
x_new = np.linspace(-10, 20, 100)[:, None]
```

**Verification:**
```python
assert np.allclose(gp._X_center, original_center), 'gp._X_center should not change after updating data for out-of-sample predictions.'
```

### Step 4: Assign _ = pm.Data(...)

```python
_ = pm.Data('X', X)
```

### Step 5: Assign cov_func = pm.gp.cov.ExpQuad(...)

```python
cov_func = pm.gp.cov.ExpQuad(1, ls=3)
```

### Step 6: Assign gp = pm.gp.HSGP(...)

```python
gp = pm.gp.HSGP(m=[20], L=[10], cov_func=cov_func)
```

### Step 7: Assign _ = gp.prior_linearized(...)

```python
_ = gp.prior_linearized(X=X)
```

### Step 8: Call pm.set_data()

```python
pm.set_data({'X': x_new})
```


## Complete Example

```python
# Workflow
X = np.linspace(0, 10, 100)[:, None]
original_center = (np.max(X, axis=0) - np.min(X, axis=0)) / 2
with pm.Model() as model:
    _ = pm.Data('X', X)
    cov_func = pm.gp.cov.ExpQuad(1, ls=3)
    gp = pm.gp.HSGP(m=[20], L=[10], cov_func=cov_func)
    _ = gp.prior_linearized(X=X)
x_new = np.linspace(-10, 20, 100)[:, None]
with model:
    pm.set_data({'X': x_new})
assert np.allclose(gp._X_center, original_center), 'gp._X_center should not change after updating data for out-of-sample predictions.'
```

## Next Steps


---

*Source: test_hsgp_approx.py:124 | Complexity: Advanced | Last updated: 2026-05-18*