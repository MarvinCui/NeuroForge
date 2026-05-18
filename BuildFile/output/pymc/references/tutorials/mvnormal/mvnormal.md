# How To: Mvnormal

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mvnormal

## Prerequisites

**Required Modules:**
- `math`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pytensor.xtensor`
- `pymc.distributions`
- `pymc`
- `pymc.dims`
- `tests.dims.utils`


## Step-by-Step Guide

### Step 1: Assign coords = value

```python
coords = {'a': range(3), 'b': range(2)}
```

**Verification:**
```python
assert_equivalent_random_graph(model, reference_model)
```

### Step 2: Assign mu = pt.as_tensor(...)

```python
mu = pt.as_tensor([1, 2])
```

**Verification:**
```python
assert_equivalent_logp_graph(model, reference_model)
```

### Step 3: Assign cov = pt.as_tensor(...)

```python
cov = pt.as_tensor([[1, 0.5], [0.5, 2]])
```

### Step 4: Assign chol = pt.as_tensor(...)

```python
chol = pt.as_tensor([[1, 0], [0.5, np.sqrt(1.75)]])
```

### Step 5: Assign mu_xr = as_xtensor(...)

```python
mu_xr = as_xtensor(mu, dims=('b',))
```

### Step 6: Assign cov_xr = as_xtensor(...)

```python
cov_xr = as_xtensor(cov, dims=('b', "b'"))
```

### Step 7: Assign chol_xr = as_xtensor(...)

```python
chol_xr = as_xtensor(chol, dims=('b', "b'"))
```

### Step 8: Call assert_equivalent_random_graph()

```python
assert_equivalent_random_graph(model, reference_model)
```

### Step 9: Call assert_equivalent_logp_graph()

```python
assert_equivalent_logp_graph(model, reference_model)
```

### Step 10: Call MvNormal()

```python
MvNormal('x', mu=mu_xr, cov=cov_xr, core_dims=('b', "b'"), dims=('a', 'b'))
```

### Step 11: Call MvNormal()

```python
MvNormal('y', mu=mu_xr, chol=chol_xr, core_dims=('b', "b'"), dims=('a', 'b'))
```

### Step 12: Call regular_distributions.MvNormal()

```python
regular_distributions.MvNormal('x', mu=mu, cov=cov, dims=('a', 'b'))
```

### Step 13: Call regular_distributions.MvNormal()

```python
regular_distributions.MvNormal('y', mu=mu, chol=chol, dims=('a', 'b'))
```


## Complete Example

```python
# Workflow
coords = {'a': range(3), 'b': range(2)}
mu = pt.as_tensor([1, 2])
cov = pt.as_tensor([[1, 0.5], [0.5, 2]])
chol = pt.as_tensor([[1, 0], [0.5, np.sqrt(1.75)]])
mu_xr = as_xtensor(mu, dims=('b',))
cov_xr = as_xtensor(cov, dims=('b', "b'"))
chol_xr = as_xtensor(chol, dims=('b', "b'"))
with Model(coords=coords) as model:
    MvNormal('x', mu=mu_xr, cov=cov_xr, core_dims=('b', "b'"), dims=('a', 'b'))
    MvNormal('y', mu=mu_xr, chol=chol_xr, core_dims=('b', "b'"), dims=('a', 'b'))
with Model(coords=coords) as reference_model:
    regular_distributions.MvNormal('x', mu=mu, cov=cov, dims=('a', 'b'))
    regular_distributions.MvNormal('y', mu=mu, chol=chol, dims=('a', 'b'))
assert_equivalent_random_graph(model, reference_model)
assert_equivalent_logp_graph(model, reference_model)
```

## Next Steps


---

*Source: test_vector.py:73 | Complexity: Advanced | Last updated: 2026-05-18*