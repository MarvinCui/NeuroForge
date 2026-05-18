# How To: T Score With Covars And Normalized Design Withcovar

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test t-scores computation with covariates.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `math`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.ndimage`
- `nilearn.conftest`
- `nilearn.mass_univariate`
- `nilearn.mass_univariate.tests._testing`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test t-scores computation with covariates.'

```python
'Test t-scores computation with covariates.'
```

**Verification:**
```python
assert_array_almost_equal(own_score, ref_score)
```

### Step 2: Assign n_samples = 50

```python
n_samples = 50
```

### Step 3: Assign var1 = value

```python
var1 = np.ones((n_samples, 1)) / np.sqrt(n_samples)
```

### Step 4: Assign var2 = rng.standard_normal(...)

```python
var2 = rng.standard_normal((n_samples, 1))
```

### Step 5: Assign var2 = value

```python
var2 = var2 / np.sqrt(np.sum(var2 ** 2, 0))
```

### Step 6: Assign covars = np.eye(...)

```python
covars = np.eye(n_samples, 3)
```

### Step 7: Assign unknown = value

```python
covars[3] = -1
```

### Step 8: Assign covars = _utils.orthonormalize_matrix(...)

```python
covars = _utils.orthonormalize_matrix(covars)
```

### Step 9: Assign own_score = _utils.t_score_with_covars_and_normalized_design(...)

```python
own_score = _utils.t_score_with_covars_and_normalized_design(var1, var2, covars)
```

### Step 10: Assign ref_score = get_tvalue_with_alternative_library(...)

```python
ref_score = get_tvalue_with_alternative_library(var1, var2, covars)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(own_score, ref_score)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test t-scores computation with covariates.'
n_samples = 50
var1 = np.ones((n_samples, 1)) / np.sqrt(n_samples)
var2 = rng.standard_normal((n_samples, 1))
var2 = var2 / np.sqrt(np.sum(var2 ** 2, 0))
covars = np.eye(n_samples, 3)
covars[3] = -1
covars = _utils.orthonormalize_matrix(covars)
own_score = _utils.t_score_with_covars_and_normalized_design(var1, var2, covars)
ref_score = get_tvalue_with_alternative_library(var1, var2, covars)
assert_array_almost_equal(own_score, ref_score)
```

## Next Steps


---

*Source: test_utils.py:247 | Complexity: Advanced | Last updated: 2026-05-18*