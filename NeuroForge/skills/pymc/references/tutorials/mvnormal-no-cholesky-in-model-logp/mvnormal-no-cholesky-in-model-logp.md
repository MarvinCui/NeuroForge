# How To: Mvnormal No Cholesky In Model Logp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test MvNormal likelihood when using Cholesky factor parameterization does not unnecessarily
recompute the cholesky factorization
Reversion test of #6717

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

### Step 1: '\n    Test MvNormal likelihood when using Cholesky factor parameterization does not unnecessarily\n    recompute the cholesky factorization\n    Reversion test of #6717\n    '

```python
'\n    Test MvNormal likelihood when using Cholesky factor parameterization does not unnecessarily\n    recompute the cholesky factorization\n    Reversion test of #6717\n    '
```

**Verification:**
```python
assert not contains_cholesky_op(logp.f.maker.fgraph)
```

### Step 2: Assign contains_cholesky_op = value

```python
contains_cholesky_op = lambda fgraph: any((isinstance(node.op, Cholesky) for node in fgraph.apply_nodes))
```

**Verification:**
```python
assert not contains_cholesky_op(dlogp.f.maker.fgraph)
```

### Step 3: Assign logp = m.compile_logp(...)

```python
logp = m.compile_logp()
```

**Verification:**
```python
assert not contains_cholesky_op(d2logp.f.maker.fgraph)
```

### Step 4: Assign dlogp = m.compile_dlogp(...)

```python
dlogp = m.compile_dlogp()
```

**Verification:**
```python
assert not contains_cholesky_op(logp_dlogp._pytensor_function.maker.fgraph)
```

### Step 5: Assign d2logp = m.compile_d2logp(...)

```python
d2logp = m.compile_d2logp()
```

**Verification:**
```python
assert not contains_cholesky_op(d2logp.f.maker.fgraph)
```

### Step 6: Assign logp_dlogp = m.logp_dlogp_function(...)

```python
logp_dlogp = m.logp_dlogp_function(ravel_inputs=True)
```

**Verification:**
```python
assert not contains_cholesky_op(logp_dlogp._pytensor_function.maker.fgraph)
```

### Step 7: Assign batch_size = 10

```python
batch_size = 10
```

### Step 8: Assign n = 3

```python
n = 3
```

### Step 9: Assign sd_dist = pm.HalfNormal.dist(...)

```python
sd_dist = pm.HalfNormal.dist(shape=n)
```

### Step 10: Assign unknown = pm.LKJCholeskyCov(...)

```python
chol, corr, sigmas = pm.LKJCholeskyCov('cov', n=n, eta=1, sd_dist=sd_dist)
```

### Step 11: Assign mu = np.zeros(...)

```python
mu = np.zeros(n)
```

### Step 12: Assign data = np.ones(...)

```python
data = np.ones((batch_size, n))
```

### Step 13: Call pm.MvNormal()

```python
pm.MvNormal('y', mu=mu, chol=pt.broadcast_to(chol, (batch_size, n, n)), observed=data)
```


## Complete Example

```python
# Workflow
'\n    Test MvNormal likelihood when using Cholesky factor parameterization does not unnecessarily\n    recompute the cholesky factorization\n    Reversion test of #6717\n    '
with pm.Model() as m:
    batch_size = 10
    n = 3
    sd_dist = pm.HalfNormal.dist(shape=n)
    chol, corr, sigmas = pm.LKJCholeskyCov('cov', n=n, eta=1, sd_dist=sd_dist)
    mu = np.zeros(n)
    data = np.ones((batch_size, n))
    pm.MvNormal('y', mu=mu, chol=pt.broadcast_to(chol, (batch_size, n, n)), observed=data)
contains_cholesky_op = lambda fgraph: any((isinstance(node.op, Cholesky) for node in fgraph.apply_nodes))
logp = m.compile_logp()
assert not contains_cholesky_op(logp.f.maker.fgraph)
dlogp = m.compile_dlogp()
assert not contains_cholesky_op(dlogp.f.maker.fgraph)
d2logp = m.compile_d2logp()
assert not contains_cholesky_op(d2logp.f.maker.fgraph)
logp_dlogp = m.logp_dlogp_function(ravel_inputs=True)
assert not contains_cholesky_op(logp_dlogp._pytensor_function.maker.fgraph)
```

## Next Steps


---

*Source: test_multivariate.py:2443 | Complexity: Advanced | Last updated: 2026-05-18*