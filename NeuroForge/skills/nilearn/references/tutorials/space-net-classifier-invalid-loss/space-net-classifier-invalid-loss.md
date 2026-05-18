# How To: Space Net Classifier Invalid Loss

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check invalid loss throw errors.

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
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Check invalid loss throw errors.'

```python
'Check invalid loss throw errors.'
```

### Step 2: Assign iris = load_iris(...)

```python
iris = load_iris()
```

### Step 3: Assign unknown = value

```python
X, y = (iris.data, iris.target)
```

### Step 4: Assign y = value

```python
y = 2 * (y > 0) - 1
```

### Step 5: Assign unknown = to_niimgs(...)

```python
X_, mask = to_niimgs(X, (2, 2, 2))
```

### Step 6: Assign alphas = value

```python
alphas = 1.0 / 0.01 / X.shape[0]
```

### Step 7: Call SpaceNetClassifier.fit()

```python
SpaceNetClassifier(mask=mask, alphas=alphas, tol=1e-10, standardize=False, screening_percentile=100.0, loss='logistic').fit(X_, y)
```

### Step 8: Call SpaceNetClassifier.fit()

```python
SpaceNetClassifier(mask=mask, alphas=alphas, tol=1e-10, standardize=False, screening_percentile=100.0, loss='mse').fit(X_, y)
```

### Step 9: Call SpaceNetClassifier.fit()

```python
SpaceNetClassifier(mask=mask, alphas=alphas, tol=1e-10, standardize=False, screening_percentile=100.0, loss='bar').fit(X_, y)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Check invalid loss throw errors.'
iris = load_iris()
X, y = (iris.data, iris.target)
y = 2 * (y > 0) - 1
X_, mask = to_niimgs(X, (2, 2, 2))
alphas = 1.0 / 0.01 / X.shape[0]
SpaceNetClassifier(mask=mask, alphas=alphas, tol=1e-10, standardize=False, screening_percentile=100.0, loss='logistic').fit(X_, y)
SpaceNetClassifier(mask=mask, alphas=alphas, tol=1e-10, standardize=False, screening_percentile=100.0, loss='mse').fit(X_, y)
with pytest.raises(ValueError, match="'loss' must be one of"):
    SpaceNetClassifier(mask=mask, alphas=alphas, tol=1e-10, standardize=False, screening_percentile=100.0, loss='bar').fit(X_, y)
```

## Next Steps


---

*Source: test_space_net.py:265 | Complexity: Advanced | Last updated: 2026-05-18*