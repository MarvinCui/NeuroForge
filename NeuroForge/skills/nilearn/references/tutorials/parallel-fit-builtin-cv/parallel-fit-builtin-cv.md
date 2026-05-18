# How To: Parallel Fit Builtin Cv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that the `fitted_param_name` output of _parallel_fit is        a single value even if param_grid is wrapped in a list        for models with built-in CV.
    

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
# Fixtures: rand_x_y, estimator, param_name, fitted_param_name, is_classification, param_values
```

## Step-by-Step Guide

### Step 1: 'Check that the `fitted_param_name` output of _parallel_fit is        a single value even if param_grid is wrapped in a list        for models with built-in CV.\n    '

```python
'Check that the `fitted_param_name` output of _parallel_fit is        a single value even if param_grid is wrapped in a list        for models with built-in CV.\n    '
```

**Verification:**
```python
assert isinstance(best_param[fitted_param_name], numbers.Number)
```

### Step 2: Assign unknown = make_regression(...)

```python
X, y = make_regression(n_samples=N_SAMPLES, n_features=20, n_informative=5, noise=0.2, random_state=42)
```

### Step 3: Assign n_samples_train = int(...)

```python
n_samples_train = int(0.8 * N_SAMPLES)
```

### Step 4: Assign train = range(...)

```python
train = range(n_samples_train)
```

### Step 5: Assign test = range(...)

```python
test = range(n_samples_train, N_SAMPLES)
```

### Step 6: Assign selector = check_feature_screening(...)

```python
selector = check_feature_screening(screening_percentile=None, mask_img=None, is_classification=False)
```

### Step 7: Assign param_grid = value

```python
param_grid = {param_name: param_values}
```

### Step 8: Assign unknown = _parallel_fit(...)

```python
_, _, _, best_param, _, _ = _parallel_fit(estimator=estimator, X=X, y=y, train=train, test=test, param_grid=param_grid, scorer=scorer, mask_img=None, class_index=1, selector=selector, clustering_percentile=100)
```

**Verification:**
```python
assert isinstance(best_param[fitted_param_name], numbers.Number)
```

### Step 9: Assign scorer = check_scoring(...)

```python
scorer = check_scoring(estimator, 'accuracy')
```

### Step 10: Assign unknown = rand_x_y

```python
_, y = rand_x_y
```

### Step 11: Assign scorer = check_scoring(...)

```python
scorer = check_scoring(estimator, 'r2')
```


## Complete Example

```python
# Setup
# Fixtures: rand_x_y, estimator, param_name, fitted_param_name, is_classification, param_values

# Workflow
'Check that the `fitted_param_name` output of _parallel_fit is        a single value even if param_grid is wrapped in a list        for models with built-in CV.\n    '
X, y = make_regression(n_samples=N_SAMPLES, n_features=20, n_informative=5, noise=0.2, random_state=42)
n_samples_train = int(0.8 * N_SAMPLES)
train = range(n_samples_train)
test = range(n_samples_train, N_SAMPLES)
selector = check_feature_screening(screening_percentile=None, mask_img=None, is_classification=False)
if is_classification:
    scorer = check_scoring(estimator, 'accuracy')
    _, y = rand_x_y
else:
    scorer = check_scoring(estimator, 'r2')
param_grid = {param_name: param_values}
_, _, _, best_param, _, _ = _parallel_fit(estimator=estimator, X=X, y=y, train=train, test=test, param_grid=param_grid, scorer=scorer, mask_img=None, class_index=1, selector=selector, clustering_percentile=100)
assert isinstance(best_param[fitted_param_name], numbers.Number)
```

## Next Steps


---

*Source: test_decoder.py:573 | Complexity: Advanced | Last updated: 2026-05-18*