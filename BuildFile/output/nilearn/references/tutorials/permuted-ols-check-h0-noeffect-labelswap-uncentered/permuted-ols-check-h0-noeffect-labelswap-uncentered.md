# How To: Permuted Ols Check H0 Noeffect Labelswap Uncentered

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check distributions of permutations when tested vars are uncentered.

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

### Step 1: 'Check distributions of permutations when tested vars are uncentered.'

```python
'Check distributions of permutations when tested vars are uncentered.'
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 3: Assign target_var = rng.randn(...)

```python
target_var = rng.randn(N_SAMPLES, 1)
```

### Step 4: Assign uncentered_var = np.arange.reshape(...)

```python
uncentered_var = np.arange(N_SAMPLES, dtype='f8').reshape((-1, 1))
```

### Step 5: Assign unknown = run_permutations(...)

```python
all_kstest_pvals, all_mse = run_permutations(uncentered_var, target_var, model_intercept=True)
```

### Step 6: Call check_ktest_p_values_distribution_and_mse()

```python
check_ktest_p_values_distribution_and_mse(all_kstest_pvals, all_mse)
```


## Complete Example

```python
# Workflow
'Check distributions of permutations when tested vars are uncentered.'
rng = np.random.RandomState(0)
target_var = rng.randn(N_SAMPLES, 1)
uncentered_var = np.arange(N_SAMPLES, dtype='f8').reshape((-1, 1))
all_kstest_pvals, all_mse = run_permutations(uncentered_var, target_var, model_intercept=True)
check_ktest_p_values_distribution_and_mse(all_kstest_pvals, all_mse)
```

## Next Steps


---

*Source: test_permuted_least_squares.py:244 | Complexity: Intermediate | Last updated: 2026-05-18*