# How To: Permuted Ols Check H0 Noeffect Labelswap Centered

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check distributions of permutations when tested vars are centered.

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
# Fixtures: model_intercept
```

## Step-by-Step Guide

### Step 1: 'Check distributions of permutations when tested vars are centered.'

```python
'Check distributions of permutations when tested vars are centered.'
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 3: Assign target_var = rng.randn(...)

```python
target_var = rng.randn(N_SAMPLES, 1)
```

### Step 4: Assign centered_var = np.arange.reshape(...)

```python
centered_var = np.arange(N_SAMPLES, dtype='f8').reshape((-1, 1))
```

### Step 5: Assign unknown = run_permutations(...)

```python
all_kstest_pvals, all_mse = run_permutations(centered_var, target_var, model_intercept=model_intercept)
```

### Step 6: Call check_ktest_p_values_distribution_and_mse()

```python
check_ktest_p_values_distribution_and_mse(all_kstest_pvals, all_mse)
```


## Complete Example

```python
# Setup
# Fixtures: model_intercept

# Workflow
'Check distributions of permutations when tested vars are centered.'
rng = np.random.RandomState(0)
target_var = rng.randn(N_SAMPLES, 1)
centered_var = np.arange(N_SAMPLES, dtype='f8').reshape((-1, 1))
centered_var -= centered_var.mean(0)
all_kstest_pvals, all_mse = run_permutations(centered_var, target_var, model_intercept=model_intercept)
check_ktest_p_values_distribution_and_mse(all_kstest_pvals, all_mse)
```

## Next Steps


---

*Source: test_permuted_least_squares.py:227 | Complexity: Intermediate | Last updated: 2026-05-18*