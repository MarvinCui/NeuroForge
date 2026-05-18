# How To: Two Sided Recover Positive And Negative Effects

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that two-sided can actually recover     positive and negative effects.
    

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

### Step 1: 'Check that two-sided can actually recover     positive and negative effects.\n    '

```python
'Check that two-sided can actually recover     positive and negative effects.\n    '
```

**Verification:**
```python
assert_array_almost_equal(output_1_sided_1['logp_max_t'][0], output_1_sided_2['logp_max_t'][0][::-1])
```

### Step 2: Assign target_var1 = np.arange.reshape(...)

```python
target_var1 = np.arange(0, 10).reshape((-1, 1))
```

**Verification:**
```python
assert_array_almost_equal(output_1_sided_1['logp_max_t'] + output_1_sided_2['logp_max_t'], output_2_sided['logp_max_t'])
```

### Step 3: Assign target_var = np.hstack(...)

```python
target_var = np.hstack((target_var1, -target_var1))
```

### Step 4: Assign tested_var = np.arange(...)

```python
tested_var = np.arange(0, 20, 2)
```

### Step 5: Assign output_1_sided_1 = permuted_ols(...)

```python
output_1_sided_1 = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=N_PERM, random_state=0)
```

### Step 6: output_1_sided_1['logp_max_t']

```python
output_1_sided_1['logp_max_t']
```

### Step 7: Assign output_1_sided_2 = permuted_ols(...)

```python
output_1_sided_2 = permuted_ols(tested_var, -target_var, model_intercept=False, two_sided_test=False, n_perm=N_PERM, random_state=0)
```

### Step 8: Assign output_2_sided = permuted_ols(...)

```python
output_2_sided = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=True, n_perm=N_PERM, random_state=0)
```

### Step 9: output_2_sided['logp_max_t']

```python
output_2_sided['logp_max_t']
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(output_1_sided_1['logp_max_t'][0], output_1_sided_2['logp_max_t'][0][::-1])
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(output_1_sided_1['logp_max_t'] + output_1_sided_2['logp_max_t'], output_2_sided['logp_max_t'])
```


## Complete Example

```python
# Workflow
'Check that two-sided can actually recover     positive and negative effects.\n    '
target_var1 = np.arange(0, 10).reshape((-1, 1))
target_var = np.hstack((target_var1, -target_var1))
tested_var = np.arange(0, 20, 2)
output_1_sided_1 = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=False, n_perm=N_PERM, random_state=0)
output_1_sided_1['logp_max_t']
output_1_sided_2 = permuted_ols(tested_var, -target_var, model_intercept=False, two_sided_test=False, n_perm=N_PERM, random_state=0)
output_2_sided = permuted_ols(tested_var, target_var, model_intercept=False, two_sided_test=True, n_perm=N_PERM, random_state=0)
output_2_sided['logp_max_t']
assert_array_almost_equal(output_1_sided_1['logp_max_t'][0], output_1_sided_2['logp_max_t'][0][::-1])
assert_array_almost_equal(output_1_sided_1['logp_max_t'] + output_1_sided_2['logp_max_t'], output_2_sided['logp_max_t'])
```

## Next Steps


---

*Source: test_permuted_least_squares.py:587 | Complexity: Advanced | Last updated: 2026-05-18*