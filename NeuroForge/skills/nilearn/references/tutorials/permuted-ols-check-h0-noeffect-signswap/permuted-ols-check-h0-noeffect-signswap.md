# How To: Permuted Ols Check H0 Noeffect Signswap

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that h0 is close to the theoretical distribution     for permuted OLS with sign swap.

Theoretical distribution is known for this simple design         (= t(n_samples - dof)).

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

### Step 1: 'Check that h0 is close to the theoretical distribution     for permuted OLS with sign swap.\n\n    Theoretical distribution is known for this simple design         (= t(n_samples - dof)).\n    '

```python
'Check that h0 is close to the theoretical distribution     for permuted OLS with sign swap.\n\n    Theoretical distribution is known for this simple design         (= t(n_samples - dof)).\n    '
```

**Verification:**
```python
assert_array_less(0.01 / (len(PERM_RANGES) * 10.0), all_kstest_pvals)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_array_less(np.diff(all_mse.mean(1)), 0)
```

### Step 3: Assign target_var = rng.randn(...)

```python
target_var = rng.randn(N_SAMPLES, 1)
```

### Step 4: Assign n_regressors = 1

```python
n_regressors = 1
```

### Step 5: Assign tested_var = np.ones(...)

```python
tested_var = np.ones((N_SAMPLES, n_regressors))
```

### Step 6: Assign unknown = run_permutations(...)

```python
all_kstest_pvals, all_mse = run_permutations(tested_var, target_var, model_intercept=False)
```

### Step 7: Assign all_kstest_pvals = np.array.reshape(...)

```python
all_kstest_pvals = np.array(all_kstest_pvals).reshape((len(PERM_RANGES), -1))
```

### Step 8: Assign all_mse = np.array.reshape(...)

```python
all_mse = np.array(all_mse).reshape((len(PERM_RANGES), -1))
```

### Step 9: Call assert_array_less()

```python
assert_array_less(0.01 / (len(PERM_RANGES) * 10.0), all_kstest_pvals)
```

### Step 10: Call assert_array_less()

```python
assert_array_less(np.diff(all_mse.mean(1)), 0)
```


## Complete Example

```python
# Workflow
'Check that h0 is close to the theoretical distribution     for permuted OLS with sign swap.\n\n    Theoretical distribution is known for this simple design         (= t(n_samples - dof)).\n    '
rng = np.random.RandomState(0)
target_var = rng.randn(N_SAMPLES, 1)
n_regressors = 1
tested_var = np.ones((N_SAMPLES, n_regressors))
all_kstest_pvals, all_mse = run_permutations(tested_var, target_var, model_intercept=False)
all_kstest_pvals = np.array(all_kstest_pvals).reshape((len(PERM_RANGES), -1))
all_mse = np.array(all_mse).reshape((len(PERM_RANGES), -1))
assert_array_less(0.01 / (len(PERM_RANGES) * 10.0), all_kstest_pvals)
assert_array_less(np.diff(all_mse.mean(1)), 0)
```

## Next Steps


---

*Source: test_permuted_least_squares.py:260 | Complexity: Advanced | Last updated: 2026-05-18*