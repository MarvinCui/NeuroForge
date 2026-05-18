# How To: Permuted Ols With Covar With Intercept

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check output when modeling intercept with normal confounds.

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
# Fixtures: design, confounding_vars
```

## Step-by-Step Guide

### Step 1: 'Check output when modeling intercept with normal confounds.'

```python
'Check output when modeling intercept with normal confounds.'
```

**Verification:**
```python
assert output['t'].shape == (n_regressors, n_descriptors)
```

### Step 2: Assign unknown = design

```python
target_var, tested_var, n_descriptors, n_regressors = design
```

**Verification:**
```python
assert ref_score.shape == (n_regressors, n_descriptors)
```

### Step 3: Assign output = permuted_ols(...)

```python
output = permuted_ols(tested_var, target_var, confounding_vars, model_intercept=True, n_perm=0, random_state=0)
```

### Step 4: Assign confounding_vars = np.hstack(...)

```python
confounding_vars = np.hstack((confounding_vars, np.ones((N_SAMPLES, 1))))
```

### Step 5: Assign ref_score = compare_to_ref_score(...)

```python
ref_score = compare_to_ref_score(output['t'], tested_var, target_var, confounding_vars)
```

**Verification:**
```python
assert output['t'].shape == (n_regressors, n_descriptors)
```


## Complete Example

```python
# Setup
# Fixtures: design, confounding_vars

# Workflow
'Check output when modeling intercept with normal confounds.'
target_var, tested_var, n_descriptors, n_regressors = design
output = permuted_ols(tested_var, target_var, confounding_vars, model_intercept=True, n_perm=0, random_state=0)
confounding_vars = np.hstack((confounding_vars, np.ones((N_SAMPLES, 1))))
ref_score = compare_to_ref_score(output['t'], tested_var, target_var, confounding_vars)
assert output['t'].shape == (n_regressors, n_descriptors)
assert ref_score.shape == (n_regressors, n_descriptors)
```

## Next Steps


---

*Source: test_permuted_least_squares.py:360 | Complexity: Intermediate | Last updated: 2026-05-18*