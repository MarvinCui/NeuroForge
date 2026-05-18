# How To: Logistic Path Scores

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logistic path scores

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign iris = load_iris(...)

```python
iris = load_iris()
```

**Verification:**
```python
assert len(test_scores) == len(alphas)
```

### Step 2: Assign unknown = value

```python
X, y = (iris.data, iris.target)
```

**Verification:**
```python
assert X.shape[1] + 1 == len(best_w)
```

### Step 3: Assign unknown = to_niimgs(...)

```python
_, mask = to_niimgs(X, [2, 2, 2])
```

### Step 4: Assign mask = get_data.astype(...)

```python
mask = get_data(mask).astype(bool)
```

### Step 5: Assign alphas = value

```python
alphas = [1.0, 0.1, 0.01]
```

### Step 6: Assign unknown = value

```python
test_scores, best_w = logistic_path_scores(graph_net_logistic, X, y, mask, alphas, 0.5, np.arange(len(X)), np.arange(len(X)), {}, verbose=0)[:2]
```

### Step 7: Assign test_scores = value

```python
test_scores = test_scores[0]
```

**Verification:**
```python
assert len(test_scores) == len(alphas)
```


## Complete Example

```python
# Workflow
iris = load_iris()
X, y = (iris.data, iris.target)
_, mask = to_niimgs(X, [2, 2, 2])
mask = get_data(mask).astype(bool)
alphas = [1.0, 0.1, 0.01]
test_scores, best_w = logistic_path_scores(graph_net_logistic, X, y, mask, alphas, 0.5, np.arange(len(X)), np.arange(len(X)), {}, verbose=0)[:2]
test_scores = test_scores[0]
assert len(test_scores) == len(alphas)
assert X.shape[1] + 1 == len(best_w)
```

## Next Steps


---

*Source: test_space_net.py:171 | Complexity: Intermediate | Last updated: 2026-05-18*