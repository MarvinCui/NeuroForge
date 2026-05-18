# How To: Check Param Grid Replacement

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test check param grid replacement

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
# Fixtures: rand_x_y, param_grid_input
```

## Step-by-Step Guide

### Step 1: Assign unknown = rand_x_y

```python
X, Y = rand_x_y
```

**Verification:**
```python
assert param_to_replace not in params
```

### Step 2: Assign param_to_replace = 'C'

```python
param_to_replace = 'C'
```

**Verification:**
```python
assert params in ParameterGrid(param_grid_input)
```

### Step 3: Assign param_replaced = 'Cs'

```python
param_replaced = 'Cs'
```

### Step 4: Assign param_grid_output = _check_param_grid(...)

```python
param_grid_output = _check_param_grid(LogisticRegressionCV(l1_ratios=(0.0,), **kwarg_logistic_regression_cv), X, Y, param_grid_input)
```

**Verification:**
```python
assert param_to_replace not in params
```

### Step 5: Assign param_grid_output = _check_param_grid(...)

```python
param_grid_output = _check_param_grid(LogisticRegressionCV(l1_ratios=(0.0,), **kwarg_logistic_regression_cv), X, Y, param_grid_input)
```

**Verification:**
```python
assert params in ParameterGrid(param_grid_input)
```


## Complete Example

```python
# Setup
# Fixtures: rand_x_y, param_grid_input

# Workflow
X, Y = rand_x_y
param_to_replace = 'C'
param_replaced = 'Cs'
if 'C' in param_grid_input or (isinstance(param_grid_input, list) and any(('C' in x for x in param_grid_input))):
    with pytest.warns(FutureWarning, match='change in the choice of underlying scikit-learn estimator'):
        param_grid_output = _check_param_grid(LogisticRegressionCV(l1_ratios=(0.0,), **kwarg_logistic_regression_cv), X, Y, param_grid_input)
else:
    param_grid_output = _check_param_grid(LogisticRegressionCV(l1_ratios=(0.0,), **kwarg_logistic_regression_cv), X, Y, param_grid_input)
for params in ParameterGrid(param_grid_output):
    assert param_to_replace not in params
    if param_replaced not in params:
        assert params in ParameterGrid(param_grid_input)
```

## Next Steps


---

*Source: test_decoder.py:297 | Complexity: Intermediate | Last updated: 2026-05-18*