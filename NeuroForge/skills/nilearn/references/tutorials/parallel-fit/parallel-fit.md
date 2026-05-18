# How To: Parallel Fit

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that results of _parallel_fit is the same     for different controlled param_grid.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `collections`
- `numbers`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn`
- `sklearn`
- `sklearn.datasets`
- `sklearn.dummy`
- `sklearn.ensemble`
- `sklearn.exceptions`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.preprocessing`
- `sklearn.svm`
- `sklearn.utils._testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.decoding`
- `nilearn.decoding._utils`
- `nilearn.decoding.decoder`
- `nilearn.decoding.tests.test_same_api`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rand_x_y
```

## Step-by-Step Guide

### Step 1: 'Check that results of _parallel_fit is the same     for different controlled param_grid.\n    '

```python
'Check that results of _parallel_fit is the same     for different controlled param_grid.\n    '
```

**Verification:**
```python
assert_array_almost_equal(a, b)
```

### Step 2: Assign unknown = make_regression(...)

```python
X, y = make_regression(n_samples=100, n_features=20, n_informative=5, noise=0.2, random_state=42)
```

**Verification:**
```python
assert a == b
```

### Step 3: Assign train = range(...)

```python
train = range(80)
```

### Step 4: Assign unknown = rand_x_y

```python
_, y_classification = rand_x_y
```

### Step 5: Assign test = range(...)

```python
test = range(80, len(y_classification))
```

### Step 6: Assign estimator = SVR(...)

```python
estimator = SVR(kernel='linear')
```

### Step 7: Assign scorer = check_scoring(...)

```python
scorer = check_scoring(estimator, 'r2')
```

### Step 8: Assign selector = check_feature_screening(...)

```python
selector = check_feature_screening(screening_percentile=None, mask_img=None, is_classification=False)
```

### Step 9: Assign outputs = value

```python
outputs = []
```

### Step 10: Assign param_grid = value

```python
param_grid = {'C': np.array(params)}
```

### Step 11: Call outputs.append()

```python
outputs.append(list(_parallel_fit(estimator=SVR(kernel='linear'), X=X, y=y, train=train, test=test, param_grid=param_grid, scorer=scorer, mask_img=None, class_index=1, selector=selector, clustering_percentile=100)))
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(a, b)
```

**Verification:**
```python
assert a == b
```


## Complete Example

```python
# Setup
# Fixtures: rand_x_y

# Workflow
'Check that results of _parallel_fit is the same     for different controlled param_grid.\n    '
X, y = make_regression(n_samples=100, n_features=20, n_informative=5, noise=0.2, random_state=42)
train = range(80)
_, y_classification = rand_x_y
test = range(80, len(y_classification))
estimator = SVR(kernel='linear')
scorer = check_scoring(estimator, 'r2')
selector = check_feature_screening(screening_percentile=None, mask_img=None, is_classification=False)
outputs = []
for params in [[0.1, 1.0, 10.0], [0.1, 1.0, 5.0, 10.0]]:
    param_grid = {'C': np.array(params)}
    outputs.append(list(_parallel_fit(estimator=SVR(kernel='linear'), X=X, y=y, train=train, test=test, param_grid=param_grid, scorer=scorer, mask_img=None, class_index=1, selector=selector, clustering_percentile=100)))
for a, b in zip(outputs[0], outputs[1], strict=False):
    if isinstance(a, np.ndarray):
        assert_array_almost_equal(a, b)
    else:
        assert a == b
```

## Next Steps


---

*Source: test_decoder.py:495 | Complexity: Advanced | Last updated: 2026-05-18*