# How To: One Sided Versus Two Test

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that a positive effect is always better     recovered with one-sided.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy`
- `nilearn.conftest`
- `nilearn.maskers`
- `nilearn.mass_univariate`
- `nilearn.mass_univariate.permuted_least_squares`
- `nilearn.mass_univariate.tests._testing`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Check that a positive effect is always better     recovered with one-sided.\n    '

```python
'Check that a positive effect is always better     recovered with one-sided.\n    '
```

**Verification:**
```python
assert output_1_sided['logp_max_t'].shape == (n_regressors, n_descriptors)
```

### Step 2: Assign n_descriptors = 100

```python
n_descriptors = 100
```

**Verification:**
```python
assert output_2_sided['logp_max_t'].shape == (n_regressors, n_descriptors)
```

### Step 3: Assign n_regressors = 1

```python
n_regressors = 1
```

**Verification:**
```python
assert_equal(np.sum(output_2_sided['logp_max_t'][positive_effect_location] - output_1_sided['logp_max_t'][positive_effect_location] > 0), 0)
```

### Step 4: Assign target_var = rng.standard_normal(...)

```python
target_var = rng.standard_normal((N_SAMPLES, n_descriptors))
```

### Step 5: Assign tested_var = rng.standard_normal(...)

```python
tested_var = rng.standard_normal((N_SAMPLES, n_regressors))
```

### Step 6: Assign output_1_sided = permuted_ols(...)

```python
output_1_sided = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=N_PERM, random_state=0)
```

**Verification:**
```python
assert output_1_sided['logp_max_t'].shape == (n_regressors, n_descriptors)
```

### Step 7: Assign output_2_sided = permuted_ols(...)

```python
output_2_sided = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=True, n_perm=N_PERM, random_state=0)
```

**Verification:**
```python
assert output_2_sided['logp_max_t'].shape == (n_regressors, n_descriptors)
```

### Step 8: Assign positive_effect_location = value

```python
positive_effect_location = output_1_sided['logp_max_t'] > 1
```

### Step 9: Call assert_equal()

```python
assert_equal(np.sum(output_2_sided['logp_max_t'][positive_effect_location] - output_1_sided['logp_max_t'][positive_effect_location] > 0), 0)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Check that a positive effect is always better     recovered with one-sided.\n    '
n_descriptors = 100
n_regressors = 1
target_var = rng.standard_normal((N_SAMPLES, n_descriptors))
tested_var = rng.standard_normal((N_SAMPLES, n_regressors))
output_1_sided = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=N_PERM, random_state=0)
assert output_1_sided['logp_max_t'].shape == (n_regressors, n_descriptors)
output_2_sided = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=True, n_perm=N_PERM, random_state=0)
assert output_2_sided['logp_max_t'].shape == (n_regressors, n_descriptors)
positive_effect_location = output_1_sided['logp_max_t'] > 1
assert_equal(np.sum(output_2_sided['logp_max_t'][positive_effect_location] - output_1_sided['logp_max_t'][positive_effect_location] > 0), 0)
```

## Next Steps


---

*Source: test_permuted_least_squares.py:545 | Complexity: Advanced | Last updated: 2026-05-18*