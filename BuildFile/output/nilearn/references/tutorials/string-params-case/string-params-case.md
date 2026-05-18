# How To: String Params Case

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check value of penalty.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `sklearn.datasets`
- `sklearn.linear_model`
- `sklearn.linear_model._coordinate_descent`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.decoding._utils`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.decoding.tests._testing`
- `nilearn.decoding.tests.test_same_api`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng, penalty_wrong_case, estimator
```

## Step-by-Step Guide

### Step 1: 'Check value of penalty.'

```python
'Check value of penalty.'
```

### Step 2: Assign dim = value

```python
dim = (4, 4, 4)
```

### Step 3: Assign W_init = np.zeros(...)

```python
W_init = np.zeros(dim)
```

### Step 4: Assign unknown = 1

```python
W_init[2:3, 1:2, -2:] = 1
```

### Step 5: Assign n = 10

```python
n = 10
```

### Step 6: Assign p = np.prod(...)

```python
p = np.prod(dim)
```

### Step 7: Assign X = value

```python
X = np.ones((n, 1)) + W_init.ravel().T
```

### Step 8: Assign y = np.dot(...)

```python
y = np.dot(X, W_init.ravel())
```

### Step 9: Assign unknown = to_niimgs(...)

```python
X, _ = to_niimgs(X, dim)
```

### Step 10: Call estimator.fit()

```python
estimator(penalty=penalty_wrong_case).fit(X, y)
```


## Complete Example

```python
# Setup
# Fixtures: rng, penalty_wrong_case, estimator

# Workflow
'Check value of penalty.'
dim = (4, 4, 4)
W_init = np.zeros(dim)
W_init[2:3, 1:2, -2:] = 1
n = 10
p = np.prod(dim)
X = np.ones((n, 1)) + W_init.ravel().T
X += rng.standard_normal((n, p))
y = np.dot(X, W_init.ravel())
X, _ = to_niimgs(X, dim)
with pytest.raises(ValueError, match="'penalty' must be one of"):
    estimator(penalty=penalty_wrong_case).fit(X, y)
```

## Next Steps


---

*Source: test_space_net.py:305 | Complexity: Advanced | Last updated: 2026-05-18*