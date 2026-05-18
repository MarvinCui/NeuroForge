# How To: Car Matrix Check

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests the check of W matrix symmetry in CARRV.make_node.

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
# Fixtures: sparse
```

## Step-by-Step Guide

### Step 1: '\n    Tests the check of W matrix symmetry in CARRV.make_node.\n    '

```python
'\n    Tests the check of W matrix symmetry in CARRV.make_node.\n    '
```

### Step 2: Call npr.seed()

```python
npr.seed(1)
```

### Step 3: Assign tau = 2

```python
tau = 2
```

### Step 4: Assign alpha = 0.5

```python
alpha = 0.5
```

### Step 5: Assign mu = np.zeros(...)

```python
mu = np.zeros(4)
```

### Step 6: Assign xs = npr.randn(...)

```python
xs = npr.randn(*mu.shape)
```

### Step 7: Assign W = np.array(...)

```python
W = np.array([[0.0, 1.0, 2.0, 0.0], [1.0, 0.0, 0.0, 1.0], [1.0, 0.0, 0.0, 1.0], [0.0, 1.0, 1.0, 0.0]])
```

### Step 8: Assign W = pytensor.tensor.as_tensor_variable(...)

```python
W = pytensor.tensor.as_tensor_variable(W)
```

### Step 9: Assign car_dist = pm.CAR.dist(...)

```python
car_dist = pm.CAR.dist(mu, W, alpha, tau)
```

### Step 10: Assign W = pytensor.sparse.csr_from_dense(...)

```python
W = pytensor.sparse.csr_from_dense(W)
```

### Step 11: Call logp.eval()

```python
logp(car_dist, xs).eval()
```

### Step 12: Assign W = np.array(...)

```python
W = np.array([0.0, 1.0, 2.0, 0.0])
```

### Step 13: Assign W = pytensor.tensor.as_tensor_variable(...)

```python
W = pytensor.tensor.as_tensor_variable(W)
```

### Step 14: Call pm.CAR.dist()

```python
pm.CAR.dist(mu, W, alpha, tau)
```


## Complete Example

```python
# Setup
# Fixtures: sparse

# Workflow
'\n    Tests the check of W matrix symmetry in CARRV.make_node.\n    '
npr.seed(1)
tau = 2
alpha = 0.5
mu = np.zeros(4)
xs = npr.randn(*mu.shape)
W = np.array([[0.0, 1.0, 2.0, 0.0], [1.0, 0.0, 0.0, 1.0], [1.0, 0.0, 0.0, 1.0], [0.0, 1.0, 1.0, 0.0]])
W = pytensor.tensor.as_tensor_variable(W)
if sparse:
    W = pytensor.sparse.csr_from_dense(W)
car_dist = pm.CAR.dist(mu, W, alpha, tau)
with pytest.raises(ParameterValueError, match='W is a symmetric adjacency matrix'):
    logp(car_dist, xs).eval()
if not sparse:
    W = np.array([0.0, 1.0, 2.0, 0.0])
    W = pytensor.tensor.as_tensor_variable(W)
    with pytest.raises(TypeError, match='W must be a matrix'):
        pm.CAR.dist(mu, W, alpha, tau)
```

## Next Steps


---

*Source: test_multivariate.py:891 | Complexity: Advanced | Last updated: 2026-05-18*