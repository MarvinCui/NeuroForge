# How To: Full Adapt Sampling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test full adapt sampling

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.sparse`
- `pymc`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`

**Setup Required:**
```python
# Fixtures: seed
```

## Step-by-Step Guide

### Step 1: Call np.random.seed()

```python
np.random.seed(seed)
```

### Step 2: Assign L = np.random.randn(...)

```python
L = np.random.randn(5, 5)
```

### Step 3: Assign unknown = np.exp(...)

```python
L[np.diag_indices_from(L)] = np.exp(L[np.diag_indices_from(L)])
```

### Step 4: Assign unknown = 0.0

```python
L[np.triu_indices_from(L, 1)] = 0.0
```

### Step 5: Call pymc.MvNormal()

```python
pymc.MvNormal('a', mu=np.zeros(len(L)), chol=L, size=len(L))
```

### Step 6: Assign initial_point = model.initial_point(...)

```python
initial_point = model.initial_point()
```

### Step 7: Assign initial_point_size = sum(...)

```python
initial_point_size = sum((initial_point[n.name].size for n in model.value_vars))
```

### Step 8: Assign step = pymc.NUTS(...)

```python
step = pymc.NUTS(model=model, potential=pot)
```

### Step 9: Assign pot = quadpotential.QuadPotentialFullAdapt(...)

```python
pot = quadpotential.QuadPotentialFullAdapt(initial_point_size, np.zeros(initial_point_size))
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
```

### Step 11: Call pymc.sample()

```python
pymc.sample(draws=10, tune=1000, random_seed=seed, step=step, cores=1, chains=1)
```


## Complete Example

```python
# Setup
# Fixtures: seed

# Workflow
np.random.seed(seed)
L = np.random.randn(5, 5)
L[np.diag_indices_from(L)] = np.exp(L[np.diag_indices_from(L)])
L[np.triu_indices_from(L, 1)] = 0.0
with pymc.Model() as model:
    pymc.MvNormal('a', mu=np.zeros(len(L)), chol=L, size=len(L))
    initial_point = model.initial_point()
    initial_point_size = sum((initial_point[n.name].size for n in model.value_vars))
    with pytest.warns(UserWarning, match='experimental feature'):
        pot = quadpotential.QuadPotentialFullAdapt(initial_point_size, np.zeros(initial_point_size))
    step = pymc.NUTS(model=model, potential=pot)
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
        pymc.sample(draws=10, tune=1000, random_seed=seed, step=step, cores=1, chains=1)
```

## Next Steps


---

*Source: test_quadpotential.py:279 | Complexity: Advanced | Last updated: 2026-05-18*