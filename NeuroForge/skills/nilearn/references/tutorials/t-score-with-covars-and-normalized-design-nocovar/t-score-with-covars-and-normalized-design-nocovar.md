# How To: T Score With Covars And Normalized Design Nocovar

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test t-scores computation without covariates.

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

### Step 1: 'Test t-scores computation without covariates.'

```python
'Test t-scores computation without covariates.'
```

**Verification:**
```python
assert_array_almost_equal(t_val_own, t_val_alt)
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

### Step 6: Assign t_val_own = _utils.t_score_with_covars_and_normalized_design(...)

```python
t_val_own = _utils.t_score_with_covars_and_normalized_design(var1, var2)
```

### Step 7: Assign t_val_alt = get_tvalue_with_alternative_library(...)

```python
t_val_alt = get_tvalue_with_alternative_library(var1, var2)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(t_val_own, t_val_alt)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test t-scores computation without covariates.'
n_samples = 50
var1 = np.ones((n_samples, 1)) / np.sqrt(n_samples)
var2 = rng.standard_normal((n_samples, 1))
var2 = var2 / np.sqrt(np.sum(var2 ** 2, 0))
t_val_own = _utils.t_score_with_covars_and_normalized_design(var1, var2)
t_val_alt = get_tvalue_with_alternative_library(var1, var2)
assert_array_almost_equal(t_val_own, t_val_alt)
```

## Next Steps


---

*Source: test_utils.py:229 | Complexity: Advanced | Last updated: 2026-05-18*