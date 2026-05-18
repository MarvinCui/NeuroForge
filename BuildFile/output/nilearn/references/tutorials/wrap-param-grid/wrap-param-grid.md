# How To: Wrap Param Grid

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test wrap param grid

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
# Fixtures: param_grid
```

## Step-by-Step Guide

### Step 1: Assign param_name = 'alphas'

```python
param_name = 'alphas'
```

**Verification:**
```python
assert isinstance(param_value, collections.abc.Iterable)
```

### Step 2: Assign original_grid = ParameterGrid(...)

```python
original_grid = ParameterGrid(param_grid)
```

**Verification:**
```python
assert all((isinstance(item, numbers.Number) for item in param_value))
```

### Step 3: Assign wrapped_grid = ParameterGrid(...)

```python
wrapped_grid = ParameterGrid(_wrap_param_grid(param_grid, param_name))
```

**Verification:**
```python
assert grid_row in original_grid
```

### Step 4: Assign param_value = value

```python
param_value = grid_row[param_name]
```

**Verification:**
```python
assert isinstance(param_value, collections.abc.Iterable)
```


## Complete Example

```python
# Setup
# Fixtures: param_grid

# Workflow
param_name = 'alphas'
original_grid = ParameterGrid(param_grid)
wrapped_grid = ParameterGrid(_wrap_param_grid(param_grid, param_name))
for grid_row in wrapped_grid:
    if param_name in grid_row:
        param_value = grid_row[param_name]
        assert isinstance(param_value, collections.abc.Iterable)
        assert all((isinstance(item, numbers.Number) for item in param_value))
    else:
        assert grid_row in original_grid
```

## Next Steps


---

*Source: test_decoder.py:368 | Complexity: Intermediate | Last updated: 2026-05-18*