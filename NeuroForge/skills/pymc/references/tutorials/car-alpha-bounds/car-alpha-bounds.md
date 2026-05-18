# How To: Car Alpha Bounds

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests the check that -1 < alpha < 1

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
# Fixtures: alpha
```

## Step-by-Step Guide

### Step 1: '\n    Tests the check that -1 < alpha < 1\n    '

```python
'\n    Tests the check that -1 < alpha < 1\n    '
```

### Step 2: Assign W = np.array(...)

```python
W = np.array([[0, 1, 0], [1, 0, 1], [0, 1, 0]])
```

### Step 3: Assign tau = 1

```python
tau = 1
```

### Step 4: Assign mu = np.array(...)

```python
mu = np.array([0, 0, 0])
```

### Step 5: Assign values = np.array(...)

```python
values = np.array([-0.5, 0, 0.5])
```

### Step 6: Assign car_dist = pm.CAR.dist(...)

```python
car_dist = pm.CAR.dist(W=W, alpha=alpha, mu=mu, tau=tau)
```

### Step 7: Call pm.draw()

```python
pm.draw(car_dist)
```

### Step 8: Call pm.logp.eval()

```python
pm.logp(car_dist, values).eval()
```


## Complete Example

```python
# Setup
# Fixtures: alpha

# Workflow
'\n    Tests the check that -1 < alpha < 1\n    '
W = np.array([[0, 1, 0], [1, 0, 1], [0, 1, 0]])
tau = 1
mu = np.array([0, 0, 0])
values = np.array([-0.5, 0, 0.5])
car_dist = pm.CAR.dist(W=W, alpha=alpha, mu=mu, tau=tau)
with pytest.raises(ValueError, match='the domain of alpha is: -1 < alpha < 1'):
    pm.draw(car_dist)
with pytest.raises(ParameterValueError, match='-1 < alpha < 1, tau > 0'):
    pm.logp(car_dist, values).eval()
```

## Next Steps


---

*Source: test_multivariate.py:922 | Complexity: Advanced | Last updated: 2026-05-18*