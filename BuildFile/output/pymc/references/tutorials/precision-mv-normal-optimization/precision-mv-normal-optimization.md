# How To: Precision Mv Normal Optimization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test precision mv normal optimization

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

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(sum(map(ord, 'be precise')))
```

**Verification:**
```python
assert not any((node for node in y_logp_fn.maker.fgraph.apply_nodes if isinstance(node.op, MatrixInverse)))
```

### Step 2: Assign n = 30

```python
n = 30
```

### Step 3: Assign L = rng.uniform(...)

```python
L = rng.uniform(low=0.1, high=1.0, size=(n, n))
```

### Step 4: Assign Sigma_test = value

```python
Sigma_test = L @ L.T
```

### Step 5: Assign mu_test = np.zeros(...)

```python
mu_test = np.zeros(n)
```

### Step 6: Assign Q_test = np.linalg.inv(...)

```python
Q_test = np.linalg.inv(Sigma_test)
```

### Step 7: Assign y_test = rng.normal(...)

```python
y_test = rng.normal(size=n)
```

### Step 8: Assign y_logp_fn = value

```python
y_logp_fn = m.compile_logp(vars=[y]).f
```

**Verification:**
```python
assert not any((node for node in y_logp_fn.maker.fgraph.apply_nodes if isinstance(node.op, MatrixInverse)))
```

### Step 9: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(y_logp_fn(y=y_test, Q=Q_test), st.multivariate_normal.logpdf(y_test, mu_test, cov=Sigma_test))
```

### Step 10: Assign Q = pm.Flat(...)

```python
Q = pm.Flat('Q', shape=(n, n))
```

### Step 11: Assign y = pm.MvNormal(...)

```python
y = pm.MvNormal('y', mu=mu_test, tau=Q)
```


## Complete Example

```python
# Workflow
rng = np.random.default_rng(sum(map(ord, 'be precise')))
n = 30
L = rng.uniform(low=0.1, high=1.0, size=(n, n))
Sigma_test = L @ L.T
mu_test = np.zeros(n)
Q_test = np.linalg.inv(Sigma_test)
y_test = rng.normal(size=n)
with Model() as m:
    Q = pm.Flat('Q', shape=(n, n))
    y = pm.MvNormal('y', mu=mu_test, tau=Q)
y_logp_fn = m.compile_logp(vars=[y]).f
assert not any((node for node in y_logp_fn.maker.fgraph.apply_nodes if isinstance(node.op, MatrixInverse)))
np.testing.assert_allclose(y_logp_fn(y=y_test, Q=Q_test), st.multivariate_normal.logpdf(y_test, mu_test, cov=Sigma_test))
```

## Next Steps


---

*Source: test_multivariate.py:2615 | Complexity: Advanced | Last updated: 2026-05-18*