# How To: Lkjcorr Default Transform

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test LKJCorr default transform

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign n = 50

```python
n = 50
```

**Verification:**
```python
assert isinstance(m.rvs_to_transforms[x], CholeskyCorrTransform)
```

### Step 2: Assign x_logp = value

```python
x_logp = m.logp(sum=False)[0]
```

**Verification:**
```python
assert x_logp.type.shape == (3,)
```

### Step 3: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng()
```

**Verification:**
```python
assert np.isfinite(fn(x_val)).all()
```

### Step 4: Assign fn = pytensor.function(...)

```python
fn = pytensor.function([m.rvs_to_values[x]], x_logp)
```

### Step 5: Assign x_val = rng.uniform(...)

```python
x_val = rng.uniform(size=(3, n * (n - 1) // 2))
```

**Verification:**
```python
assert np.isfinite(fn(x_val)).all()
```

### Step 6: Assign x = pm.LKJCorr(...)

```python
x = pm.LKJCorr('x', n=n, eta=1, shape=(3, n, n))
```


## Complete Example

```python
# Workflow
n = 50
with pm.Model() as m:
    x = pm.LKJCorr('x', n=n, eta=1, shape=(3, n, n))
assert isinstance(m.rvs_to_transforms[x], CholeskyCorrTransform)
x_logp = m.logp(sum=False)[0]
assert x_logp.type.shape == (3,)
rng = np.random.default_rng()
fn = pytensor.function([m.rvs_to_values[x]], x_logp)
x_val = rng.uniform(size=(3, n * (n - 1) // 2))
assert np.isfinite(fn(x_val)).all()
```

## Next Steps


---

*Source: test_multivariate.py:2291 | Complexity: Intermediate | Last updated: 2026-05-18*