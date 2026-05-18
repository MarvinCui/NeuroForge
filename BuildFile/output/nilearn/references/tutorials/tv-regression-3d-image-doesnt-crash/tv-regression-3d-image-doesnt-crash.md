# How To: Tv Regression 3D Image Doesnt Crash

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test tv regression 3d image doesnt crash

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
# Fixtures: rng, l1_ratio
```

## Step-by-Step Guide

### Step 1: Assign dim = value

```python
dim = (3, 4, 5)
```

### Step 2: Assign W_init = np.zeros(...)

```python
W_init = np.zeros(dim)
```

### Step 3: Assign unknown = 1

```python
W_init[2:3, 3:, 1:3] = 1
```

### Step 4: Assign n = 10

```python
n = 10
```

### Step 5: Assign p = value

```python
p = dim[0] * dim[1] * dim[2]
```

### Step 6: Assign X = value

```python
X = np.ones((n, 1)) + W_init.ravel().T
```

### Step 7: Assign y = np.dot(...)

```python
y = np.dot(X, W_init.ravel())
```

### Step 8: Assign alpha = 1.0

```python
alpha = 1.0
```

### Step 9: Assign unknown = to_niimgs(...)

```python
X, mask = to_niimgs(X, dim)
```

### Step 10: Call SpaceNetRegressor.fit()

```python
SpaceNetRegressor(mask=mask, alphas=alpha, l1_ratios=l1_ratio, penalty='tv-l1', max_iter=10, standardize='zscore_sample').fit(X, y)
```


## Complete Example

```python
# Setup
# Fixtures: rng, l1_ratio

# Workflow
dim = (3, 4, 5)
W_init = np.zeros(dim)
W_init[2:3, 3:, 1:3] = 1
n = 10
p = dim[0] * dim[1] * dim[2]
X = np.ones((n, 1)) + W_init.ravel().T
X += rng.standard_normal((n, p))
y = np.dot(X, W_init.ravel())
alpha = 1.0
X, mask = to_niimgs(X, dim)
SpaceNetRegressor(mask=mask, alphas=alpha, l1_ratios=l1_ratio, penalty='tv-l1', max_iter=10, standardize='zscore_sample').fit(X, y)
```

## Next Steps


---

*Source: test_space_net.py:321 | Complexity: Advanced | Last updated: 2026-05-18*