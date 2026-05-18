# How To: Lkjcorr

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test lkjcorr

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `warnings`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytest`
- `scipy.special`
- `scipy.stats`
- `pytensor`
- `pytensor.compile.mode`
- `pytensor.tensor`
- `pytensor.tensor.blockwise`
- `pytensor.tensor.linalg.decomposition.cholesky`
- `pytensor.tensor.linalg.inverse`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.utils`
- `pymc`
- `pymc`
- `pymc.distributions.multivariate`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.math`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: x_tri, eta, n, lp
```

## Step-by-Step Guide

### Step 1: Assign x = np.eye(...)

```python
x = np.eye(n)
```

### Step 2: Assign unknown = x_tri

```python
x[np.tril_indices(n, -1)] = x_tri
```

### Step 3: Assign unknown = x_tri

```python
x[np.triu_indices(n, 1)] = x_tri
```

### Step 4: Assign point = value

```python
point = {'lkj': x_chol}
```

### Step 5: Assign decimals = select_by_precision(...)

```python
decimals = select_by_precision(float64=6, float32=4)
```

### Step 6: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(model.compile_logp()(point), lp, decimal=decimals, err_msg=str(point))
```

### Step 7: Call pm.LKJCorr()

```python
pm.LKJCorr('lkj', eta=eta, n=n, transform=None)
```

### Step 8: Assign x_chol = np.linalg.cholesky(...)

```python
x_chol = np.linalg.cholesky(x)
```

### Step 9: Assign x_chol = x

```python
x_chol = x
```


## Complete Example

```python
# Setup
# Fixtures: x_tri, eta, n, lp

# Workflow
with pm.Model() as model:
    pm.LKJCorr('lkj', eta=eta, n=n, transform=None)
x = np.eye(n)
x[np.tril_indices(n, -1)] = x_tri
x[np.triu_indices(n, 1)] = x_tri
try:
    x_chol = np.linalg.cholesky(x)
except np.linalg.LinAlgError:
    x_chol = x
point = {'lkj': x_chol}
decimals = select_by_precision(float64=6, float32=4)
npt.assert_almost_equal(model.compile_logp()(point), lp, decimal=decimals, err_msg=str(point))
```

## Next Steps


---

*Source: test_multivariate.py:560 | Complexity: Advanced | Last updated: 2026-05-18*