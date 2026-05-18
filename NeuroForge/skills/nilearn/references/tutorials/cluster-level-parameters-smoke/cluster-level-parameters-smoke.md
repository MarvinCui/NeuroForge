# How To: Cluster Level Parameters Smoke

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test combinations of parameters related to cluster-level inference.

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
# Fixtures: cluster_level_design, masker
```

## Step-by-Step Guide

### Step 1: 'Test combinations of parameters related to cluster-level inference.'

```python
'Test combinations of parameters related to cluster-level inference.'
```

**Verification:**
```python
assert isinstance(out, dict)
```

### Step 2: Assign unknown = cluster_level_design

```python
target_var, tested_var = cluster_level_design
```

**Verification:**
```python
assert 't' in out
```

### Step 3: Assign out = permuted_ols(...)

```python
out = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=0, random_state=0)
```

**Verification:**
```python
assert isinstance(out, dict)
```

### Step 4: Assign n_perm = N_PERM

```python
n_perm = N_PERM
```

**Verification:**
```python
assert 't' in out
```

### Step 5: Assign out = permuted_ols(...)

```python
out = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=True, n_perm=n_perm, random_state=0, threshold=0.001, masker=masker)
```

**Verification:**
```python
assert 'logp_max_t' in out
```


## Complete Example

```python
# Setup
# Fixtures: cluster_level_design, masker

# Workflow
'Test combinations of parameters related to cluster-level inference.'
target_var, tested_var = cluster_level_design
out = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=0, random_state=0)
assert isinstance(out, dict)
assert 't' in out
n_perm = N_PERM
out = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=True, n_perm=n_perm, random_state=0, threshold=0.001, masker=masker)
assert isinstance(out, dict)
assert 't' in out
assert 'logp_max_t' in out
assert 'logp_max_size' in out
assert 'logp_max_mass' in out
assert 'h0_max_t' in out
assert 'h0_max_size' in out
assert 'h0_max_mass' in out
assert out['h0_max_t'].size == n_perm
assert out['h0_max_size'].size == n_perm
assert out['h0_max_mass'].size == n_perm
```

## Next Steps


---

*Source: test_permuted_least_squares.py:697 | Complexity: Intermediate | Last updated: 2026-05-18*