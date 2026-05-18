# How To: Multivariate Transform

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multivariate transform

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.graph`
- `pytensor.graph.rewriting.basic`
- `pytensor.tensor.exceptions`
- `pymc`
- `pymc.distributions.shape_utils`
- `pymc.model.fgraph`


## Step-by-Step Guide

### Step 1: Assign new_m = clone_model(...)

```python
new_m = clone_model(m)
```

### Step 2: Assign ip = m.initial_point(...)

```python
ip = m.initial_point()
```

### Step 3: Assign new_ip = new_m.initial_point(...)

```python
new_ip = new_m.initial_point()
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(ip['x_simplex__'], new_ip['x_simplex__'])
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(ip['y_cholesky-cov-packed__'], new_ip['y_cholesky-cov-packed__'])
```

### Step 6: Assign x = pm.Dirichlet(...)

```python
x = pm.Dirichlet('x', a=[1, 1, 1])
```

### Step 7: Assign unknown = pm.LKJCholeskyCov(...)

```python
y, *_ = pm.LKJCholeskyCov('y', n=4, eta=1, sd_dist=pm.Exponential.dist(1))
```


## Complete Example

```python
# Workflow
with pm.Model() as m:
    x = pm.Dirichlet('x', a=[1, 1, 1])
    y, *_ = pm.LKJCholeskyCov('y', n=4, eta=1, sd_dist=pm.Exponential.dist(1))
new_m = clone_model(m)
ip = m.initial_point()
new_ip = new_m.initial_point()
np.testing.assert_allclose(ip['x_simplex__'], new_ip['x_simplex__'])
np.testing.assert_allclose(ip['y_cholesky-cov-packed__'], new_ip['y_cholesky-cov-packed__'])
```

## Next Steps


---

*Source: test_fgraph.py:389 | Complexity: Intermediate | Last updated: 2026-05-18*