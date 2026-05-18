# How To: Permutation T Test

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test T-test based on permutations.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne.fixes`
- `mne.stats`
- `mne.stats.permutations`


## Step-by-Step Guide

### Step 1: 'Test T-test based on permutations.'

```python
'Test T-test based on permutations.'
```

**Verification:**
```python
assert (p_values > 0).all()
```

### Step 2: Call np.random.seed()

```python
np.random.seed(10)
```

**Verification:**
```python
assert len(H0) == 999
```

### Step 3: Assign unknown = value

```python
n_samples, n_tests = (30, 5)
```

**Verification:**
```python
assert_array_equal(is_significant, [True, True, False, False, False])
```

### Step 4: Assign X = np.random.randn(...)

```python
X = np.random.randn(n_samples, n_tests)
```

**Verification:**
```python
assert (p_values > 0).all()
```

### Step 5: Assign unknown = permutation_t_test(...)

```python
t_obs, p_values, H0 = permutation_t_test(X, n_permutations=999, tail=0, seed=0)
```

**Verification:**
```python
assert len(H0) == 999
```

### Step 6: Assign is_significant = value

```python
is_significant = p_values < 0.05
```

**Verification:**
```python
assert_array_equal(is_significant, [True, True, False, False, False])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(is_significant, [True, True, False, False, False])
```

**Verification:**
```python
assert_array_equal(is_significant, [False, False, False, False, False])
```

### Step 8: Assign unknown = permutation_t_test(...)

```python
t_obs, p_values, H0 = permutation_t_test(X, n_permutations=999, tail=1, seed=0)
```

**Verification:**
```python
assert (p_values > 0).all()
```

### Step 9: Assign is_significant = value

```python
is_significant = p_values < 0.05
```

**Verification:**
```python
assert len(H0) == 999
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(is_significant, [True, True, False, False, False])
```

**Verification:**
```python
assert_array_equal(is_significant, [True, True, False, False, False])
```

### Step 11: Assign unknown = permutation_t_test(...)

```python
t_obs, p_values, H0 = permutation_t_test(X, n_permutations=999, tail=-1, seed=0)
```

**Verification:**
```python
assert_allclose(t_obs_clust, t_obs)
```

### Step 12: Assign is_significant = value

```python
is_significant = p_values < 0.05
```

**Verification:**
```python
assert_allclose(p_values_clust, p_values[keep], atol=0.01)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(is_significant, [False, False, False, False, False])
```

### Step 14: Assign unknown = permutation_t_test(...)

```python
t_obs, p_values, H0 = permutation_t_test(X, n_permutations=999, tail=-1, seed=0)
```

**Verification:**
```python
assert (p_values > 0).all()
```

### Step 15: Assign is_significant = value

```python
is_significant = p_values < 0.05
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(is_significant, [True, True, False, False, False])
```

### Step 17: Assign unknown = permutation_cluster_1samp_test(...)

```python
t_obs_clust, _, p_values_clust, _ = permutation_cluster_1samp_test(X, n_permutations=999, seed=0, adjacency=adjacency, out_type='mask')
```

### Step 18: Assign keep = value

```python
keep = p_values < 1
```

### Step 19: Call assert_allclose()

```python
assert_allclose(t_obs_clust, t_obs)
```

### Step 20: Call assert_allclose()

```python
assert_allclose(p_values_clust, p_values[keep], atol=0.01)
```


## Complete Example

```python
# Workflow
'Test T-test based on permutations.'
np.random.seed(10)
n_samples, n_tests = (30, 5)
X = np.random.randn(n_samples, n_tests)
X[:, :2] += 1
t_obs, p_values, H0 = permutation_t_test(X, n_permutations=999, tail=0, seed=0)
assert (p_values > 0).all()
assert len(H0) == 999
is_significant = p_values < 0.05
assert_array_equal(is_significant, [True, True, False, False, False])
t_obs, p_values, H0 = permutation_t_test(X, n_permutations=999, tail=1, seed=0)
assert (p_values > 0).all()
assert len(H0) == 999
is_significant = p_values < 0.05
assert_array_equal(is_significant, [True, True, False, False, False])
t_obs, p_values, H0 = permutation_t_test(X, n_permutations=999, tail=-1, seed=0)
is_significant = p_values < 0.05
assert_array_equal(is_significant, [False, False, False, False, False])
X *= -1
t_obs, p_values, H0 = permutation_t_test(X, n_permutations=999, tail=-1, seed=0)
assert (p_values > 0).all()
assert len(H0) == 999
is_significant = p_values < 0.05
assert_array_equal(is_significant, [True, True, False, False, False])
for adjacency in (_eye_array(n_tests), False):
    t_obs_clust, _, p_values_clust, _ = permutation_cluster_1samp_test(X, n_permutations=999, seed=0, adjacency=adjacency, out_type='mask')
    keep = p_values < 1
    assert_allclose(t_obs_clust, t_obs)
    assert_allclose(p_values_clust, p_values[keep], atol=0.01)
```

## Next Steps


---

*Source: test_permutations.py:19 | Complexity: Advanced | Last updated: 2026-05-18*