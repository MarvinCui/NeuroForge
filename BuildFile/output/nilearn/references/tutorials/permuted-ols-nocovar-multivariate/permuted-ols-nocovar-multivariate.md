# How To: Permuted Ols Nocovar Multivariate

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test permuted_ols with multiple tested variates and no covariate.

It is equivalent to fitting several models with only one tested variate.

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

### Step 1: 'Test permuted_ols with multiple tested variates and no covariate.\n\n    It is equivalent to fitting several models with only one tested variate.\n    '

```python
'Test permuted_ols with multiple tested variates and no covariate.\n\n    It is equivalent to fitting several models with only one tested variate.\n    '
```

**Verification:**
```python
assert output['logp_max_t'].shape == (n_regressors, n_descriptors)
```

### Step 2: Assign n_descriptors = 10

```python
n_descriptors = 10
```

**Verification:**
```python
assert output['h0_max_t'].shape == (n_regressors, n_perm)
```

### Step 3: Assign n_regressors = 2

```python
n_regressors = 2
```

### Step 4: Assign unknown = _create_design(...)

```python
target_vars, tested_var, *_ = _create_design(rng, n_samples=N_SAMPLES, n_descriptors=n_descriptors, n_regressors=n_regressors)
```

### Step 5: Assign n_perm = N_PERM

```python
n_perm = N_PERM
```

### Step 6: Assign output = permuted_ols(...)

```python
output = permuted_ols(tested_var, target_vars, model_intercept=False, n_perm=n_perm, random_state=0)
```

### Step 7: Call compare_to_ref_score()

```python
compare_to_ref_score(output['t'], tested_var, target_vars)
```

**Verification:**
```python
assert output['logp_max_t'].shape == (n_regressors, n_descriptors)
```

### Step 8: Assign output_intercept = permuted_ols(...)

```python
output_intercept = permuted_ols(tested_var, target_vars, model_intercept=True, n_perm=0, random_state=0)
```

### Step 9: Call compare_to_ref_score()

```python
compare_to_ref_score(output_intercept['t'], tested_var, target_vars, np.ones((N_SAMPLES, 1)))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test permuted_ols with multiple tested variates and no covariate.\n\n    It is equivalent to fitting several models with only one tested variate.\n    '
n_descriptors = 10
n_regressors = 2
target_vars, tested_var, *_ = _create_design(rng, n_samples=N_SAMPLES, n_descriptors=n_descriptors, n_regressors=n_regressors)
n_perm = N_PERM
output = permuted_ols(tested_var, target_vars, model_intercept=False, n_perm=n_perm, random_state=0)
compare_to_ref_score(output['t'], tested_var, target_vars)
assert output['logp_max_t'].shape == (n_regressors, n_descriptors)
assert output['h0_max_t'].shape == (n_regressors, n_perm)
output_intercept = permuted_ols(tested_var, target_vars, model_intercept=True, n_perm=0, random_state=0)
target_vars -= target_vars.mean(0)
tested_var -= tested_var.mean(0)
compare_to_ref_score(output_intercept['t'], tested_var, target_vars, np.ones((N_SAMPLES, 1)))
```

## Next Steps


---

*Source: test_permuted_least_squares.py:422 | Complexity: Advanced | Last updated: 2026-05-18*