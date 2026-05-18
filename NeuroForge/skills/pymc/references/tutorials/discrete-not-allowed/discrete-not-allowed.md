# How To: Discrete Not Allowed

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test discrete not allowed

## Prerequisites

**Required Modules:**
- `functools`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.testing`
- `pymc.variational`
- `pymc.variational.approximations`
- `tests.helpers`
- `cloudpickle`
- `cloudpickle`


## Step-by-Step Guide

### Step 1: Assign mu_true = np.array(...)

```python
mu_true = np.array([-2, 0, 2])
```

### Step 2: Assign z_true = np.random.randint(...)

```python
z_true = np.random.randint(len(mu_true), size=100)
```

### Step 3: Assign y = np.random.normal(...)

```python
y = np.random.normal(mu_true[z_true], np.ones_like(z_true))
```

### Step 4: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', mu=0, sigma=10, size=3)
```

### Step 5: Assign z = pm.Categorical(...)

```python
z = pm.Categorical('z', p=pt.ones(3) / 3, size=len(y))
```

### Step 6: Call pm.Normal()

```python
pm.Normal('y_obs', mu=mu[z], sigma=1.0, observed=y)
```

### Step 7: Call pm.fit()

```python
pm.fit(n=1)
```


## Complete Example

```python
# Workflow
mu_true = np.array([-2, 0, 2])
z_true = np.random.randint(len(mu_true), size=100)
y = np.random.normal(mu_true[z_true], np.ones_like(z_true))
with pm.Model():
    mu = pm.Normal('mu', mu=0, sigma=10, size=3)
    z = pm.Categorical('z', p=pt.ones(3) / 3, size=len(y))
    pm.Normal('y_obs', mu=mu[z], sigma=1.0, observed=y)
    with pytest.raises(opvi.ParametrizationError, match='Discrete variables'):
        pm.fit(n=1)
```

## Next Steps


---

*Source: test_opvi.py:36 | Complexity: Intermediate | Last updated: 2026-05-18*