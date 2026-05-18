# How To: Tv Regression Simple

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test tv regression simple

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
# Fixtures: rng, l1_ratio, debias
```

## Step-by-Step Guide

### Step 1: Assign dim = value

```python
dim = (4, 4, 4)
```

### Step 2: Assign W_init = np.zeros(...)

```python
W_init = np.zeros(dim)
```

### Step 3: Assign unknown = 1

```python
W_init[2:3, 1:2, -2:] = 1
```

### Step 4: Assign n = 10

```python
n = 10
```

### Step 5: Assign p = np.prod(...)

```python
p = np.prod(dim)
```

### Step 6: Assign X = value

```python
X = np.ones((n, 1)) + W_init.ravel().T
```

### Step 7: Assign y = np.dot(...)

```python
y = np.dot(X, W_init.ravel())
```

### Step 8: Assign unknown = to_niimgs(...)

```python
X, mask = to_niimgs(X, dim)
```

### Step 9: Assign alphas = value

```python
alphas = [0.1, 1.0]
```

### Step 10: Call SpaceNetRegressor.fit()

```python
SpaceNetRegressor(mask=mask, alphas=alphas, l1_ratios=l1_ratio, penalty='tv-l1', max_iter=10, debias=debias, standardize='zscore_sample').fit(X, y)
```


## Complete Example

```python
# Setup
# Fixtures: rng, l1_ratio, debias

# Workflow
dim = (4, 4, 4)
W_init = np.zeros(dim)
W_init[2:3, 1:2, -2:] = 1
n = 10
p = np.prod(dim)
X = np.ones((n, 1)) + W_init.ravel().T
X += rng.standard_normal((n, p))
y = np.dot(X, W_init.ravel())
X, mask = to_niimgs(X, dim)
alphas = [0.1, 1.0]
SpaceNetRegressor(mask=mask, alphas=alphas, l1_ratios=l1_ratio, penalty='tv-l1', max_iter=10, debias=debias, standardize='zscore_sample').fit(X, y)
```

## Next Steps


---

*Source: test_space_net.py:223 | Complexity: Advanced | Last updated: 2026-05-18*