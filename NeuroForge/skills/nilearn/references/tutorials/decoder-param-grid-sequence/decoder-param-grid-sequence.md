# How To: Decoder Param Grid Sequence

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test decoder param grid sequence

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
# Fixtures: binary_classification_data
```

## Step-by-Step Guide

### Step 1: Assign unknown = binary_classification_data

```python
X, y, _ = binary_classification_data
```

**Verification:**
```python
assert len(param_list) == n_cv_folds
```

### Step 2: Assign n_cv_folds = 10

```python
n_cv_folds = 10
```

### Step 3: Assign param_grid = value

```python
param_grid = [{'penalty': ['l2'], 'C': [100, 1000], 'random_state': [42]}, {'penalty': ['l1'], 'dual': [False], 'C': [100, 10], 'random_state': [42]}]
```

### Step 4: Assign model = Decoder(...)

```python
model = Decoder(param_grid=param_grid, cv=n_cv_folds, standardize='zscore_sample')
```

### Step 5: Call model.fit()

```python
model.fit(X, y)
```

**Verification:**
```python
assert len(param_list) == n_cv_folds
```


## Complete Example

```python
# Setup
# Fixtures: binary_classification_data

# Workflow
X, y, _ = binary_classification_data
n_cv_folds = 10
param_grid = [{'penalty': ['l2'], 'C': [100, 1000], 'random_state': [42]}, {'penalty': ['l1'], 'dual': [False], 'C': [100, 10], 'random_state': [42]}]
model = Decoder(param_grid=param_grid, cv=n_cv_folds, standardize='zscore_sample')
model.fit(X, y)
for best_params in model.cv_params_.values():
    for param_list in best_params.values():
        assert len(param_list) == n_cv_folds
```

## Next Steps


---

*Source: test_decoder.py:629 | Complexity: Intermediate | Last updated: 2026-05-18*