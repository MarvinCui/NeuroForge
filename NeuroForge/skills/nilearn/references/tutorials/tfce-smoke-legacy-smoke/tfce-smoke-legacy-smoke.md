# How To: Tfce Smoke Legacy Smoke

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check tfce output of dict with or without permutations.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Check tfce output of dict with or without permutations.'

```python
'Check tfce output of dict with or without permutations.'
```

**Verification:**
```python
assert isinstance(out, dict)
```

### Step 2: Assign unknown = _tfce_design(...)

```python
target_var, tested_var, masker, n_descriptors, n_regressors = _tfce_design()
```

**Verification:**
```python
assert 't' in out
```

### Step 3: Assign out = permuted_ols(...)

```python
out = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=0, random_state=0, masker=masker, tfce=True)
```

**Verification:**
```python
assert 'tfce' in out
```

### Step 4: Assign n_perm = N_PERM

```python
n_perm = N_PERM
```

**Verification:**
```python
assert out['t'].shape == (n_regressors, n_descriptors)
```

### Step 5: Assign out = permuted_ols(...)

```python
out = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=n_perm, random_state=0, masker=masker, tfce=True)
```

**Verification:**
```python
assert out['tfce'].shape == (n_regressors, n_descriptors)
```


## Complete Example

```python
# Workflow
'Check tfce output of dict with or without permutations.'
target_var, tested_var, masker, n_descriptors, n_regressors = _tfce_design()
out = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=0, random_state=0, masker=masker, tfce=True)
assert isinstance(out, dict)
assert 't' in out
assert 'tfce' in out
assert out['t'].shape == (n_regressors, n_descriptors)
assert out['tfce'].shape == (n_regressors, n_descriptors)
n_perm = N_PERM
out = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=n_perm, random_state=0, masker=masker, tfce=True)
assert isinstance(out, dict)
assert 't' in out
assert 'tfce' in out
assert 'logp_max_t' in out
assert 'logp_max_tfce' in out
assert 'h0_max_t' in out
assert 'h0_max_tfce' in out
assert out['t'].shape == (n_regressors, n_descriptors)
assert out['tfce'].shape == (n_regressors, n_descriptors)
assert out['logp_max_t'].shape == (n_regressors, n_descriptors)
assert out['logp_max_tfce'].shape == (n_regressors, n_descriptors)
assert out['h0_max_t'].size == n_perm
assert out['h0_max_tfce'].size == n_perm
```

## Next Steps


---

*Source: test_permuted_least_squares.py:638 | Complexity: Intermediate | Last updated: 2026-05-18*