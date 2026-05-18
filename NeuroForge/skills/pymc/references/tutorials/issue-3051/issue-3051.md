# How To: Issue 3051

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test issue 3051

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `warnings`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pytensor`
- `pytensor.tensor`
- `pytensor.tensor.random.utils`
- `pymc`
- `pymc.distributions`
- `pymc.distributions.distribution`
- `pymc.distributions.shape_utils`
- `pymc.logprob.basic`
- `pymc.pytensorf`
- `pymc.testing`
- `pymc.distributions`
- `pymc.distributions.distribution`
- `pymc.distributions.dist_math`
- `pymc.distributions.distribution`

**Setup Required:**
```python
# Fixtures: dims, dist_cls, kwargs
```

## Step-by-Step Guide

### Step 1: Assign mu = np.repeat(...)

```python
mu = np.repeat(0, dims)
```

**Verification:**
```python
assert isinstance(actual_t, TensorVariable)
```

### Step 2: Assign d = dist_cls.dist(...)

```python
d = dist_cls.dist(mu=mu, cov=np.eye(dims), **kwargs, size=20)
```

**Verification:**
```python
assert isinstance(actual_a, np.ndarray)
```

### Step 3: Assign X = npr.normal(...)

```python
X = npr.normal(size=(20, dims))
```

**Verification:**
```python
assert actual_a.shape == (X.shape[0],)
```

### Step 4: Assign actual_t = logp(...)

```python
actual_t = logp(d, X)
```

**Verification:**
```python
assert isinstance(actual_t, TensorVariable)
```

### Step 5: Assign actual_a = actual_t.eval(...)

```python
actual_a = actual_t.eval()
```

**Verification:**
```python
assert isinstance(actual_a, np.ndarray)
```


## Complete Example

```python
# Setup
# Fixtures: dims, dist_cls, kwargs

# Workflow
mu = np.repeat(0, dims)
d = dist_cls.dist(mu=mu, cov=np.eye(dims), **kwargs, size=20)
X = npr.normal(size=(20, dims))
actual_t = logp(d, X)
assert isinstance(actual_t, TensorVariable)
actual_a = actual_t.eval()
assert isinstance(actual_a, np.ndarray)
assert actual_a.shape == (X.shape[0],)
```

## Next Steps


---

*Source: test_distribution.py:60 | Complexity: Intermediate | Last updated: 2026-05-18*