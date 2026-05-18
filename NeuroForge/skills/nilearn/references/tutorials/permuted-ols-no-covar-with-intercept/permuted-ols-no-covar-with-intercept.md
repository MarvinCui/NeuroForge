# How To: Permuted Ols No Covar With Intercept

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check output when modeling intercept with no confounds.

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
# Fixtures: design
```

## Step-by-Step Guide

### Step 1: 'Check output when modeling intercept with no confounds.'

```python
'Check output when modeling intercept with no confounds.'
```

### Step 2: Assign unknown = design

```python
target_var, tested_var, *_ = design
```

### Step 3: Assign output = permuted_ols(...)

```python
output = permuted_ols(tested_var, target_var, model_intercept=True, n_perm=0, random_state=0)
```

### Step 4: Call compare_to_ref_score()

```python
compare_to_ref_score(output['t'], tested_var, target_var, np.ones((N_SAMPLES, 1)))
```


## Complete Example

```python
# Setup
# Fixtures: design

# Workflow
'Check output when modeling intercept with no confounds.'
target_var, tested_var, *_ = design
output = permuted_ols(tested_var, target_var, model_intercept=True, n_perm=0, random_state=0)
target_var -= target_var.mean(0)
tested_var -= tested_var.mean(0)
compare_to_ref_score(output['t'], tested_var, target_var, np.ones((N_SAMPLES, 1)))
```

## Next Steps


---

*Source: test_permuted_least_squares.py:320 | Complexity: Intermediate | Last updated: 2026-05-18*