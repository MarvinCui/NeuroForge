# How To: Cluster Permutation T Test

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test cluster level permutations T-test.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `functools`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.fixes`
- `mne.stats`
- `mne.stats.cluster_level`
- `mne.utils`
- `sklearn.feature_extraction.image`
- `sklearn.feature_extraction.image`
- `sklearn.feature_extraction.image`

**Setup Required:**
```python
# Fixtures: numba_conditional, stat_fun
```

## Step-by-Step Guide

### Step 1: 'Test cluster level permutations T-test.'

```python
'Test cluster level permutations T-test.'
```

**Verification:**
```python
assert_equal(np.sum(cluster_p_values < 0.05), 1)
```

### Step 2: Assign unknown = _get_conditions(...)

```python
condition1_1d, _, condition1_2d, _ = _get_conditions()
```

**Verification:**
```python
assert_allclose(p_min, p, atol=1e-06)
```

### Step 3: Assign unknown = permutation_cluster_1samp_test(...)

```python
T_obs, clusters, cluster_p_values, hist = permutation_cluster_1samp_test(condition1, n_permutations=100, tail=0, seed=1, out_type='mask', buffer_size=None)
```

**Verification:**
```python
assert_array_equal(T_obs_pos, -T_obs_neg)
```

### Step 4: Call assert_equal()

```python
assert_equal(np.sum(cluster_p_values < 0.05), 1)
```

**Verification:**
```python
assert_array_equal(cluster_p_values_pos < 0.05, cluster_p_values_neg < 0.05)
```

### Step 5: Assign p_min = np.min(...)

```python
p_min = np.min(cluster_p_values)
```

**Verification:**
```python
assert_array_equal(T_obs_neg, T_obs_neg_buff)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(p_min, p, atol=1e-06)
```

**Verification:**
```python
assert_array_equal(cluster_p_values_neg, cluster_p_values_neg_buff)
```

### Step 7: Assign unknown = permutation_cluster_1samp_test(...)

```python
T_obs_pos, _, cluster_p_values_pos, _ = permutation_cluster_1samp_test(condition1, n_permutations=100, tail=1, threshold=1.67, seed=1, stat_fun=stat_fun, out_type='mask', buffer_size=None)
```

### Step 8: Assign unknown = permutation_cluster_1samp_test(...)

```python
T_obs_neg, _, cluster_p_values_neg, _ = permutation_cluster_1samp_test(-condition1, n_permutations=100, tail=-1, threshold=-1.67, seed=1, stat_fun=stat_fun, buffer_size=None, out_type='mask')
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(T_obs_pos, -T_obs_neg)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(cluster_p_values_pos < 0.05, cluster_p_values_neg < 0.05)
```

### Step 11: Assign buffer_size = value

```python
buffer_size = condition1.shape[1] // 10
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(T_obs_neg, T_obs_neg_buff)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(cluster_p_values_neg, cluster_p_values_neg_buff)
```

### Step 14: Assign unknown = permutation_cluster_1samp_test(...)

```python
T_obs_neg_buff, _, cluster_p_values_neg_buff, _ = permutation_cluster_1samp_test(-condition1, n_permutations=100, tail=-1, out_type='mask', threshold=-1.67, seed=1, n_jobs=2, stat_fun=stat_fun, buffer_size=buffer_size)
```

### Step 15: Call permutation_cluster_1samp_test()

```python
permutation_cluster_1samp_test(condition1, threshold=1, stat_fun=lambda x: None, out_type='mask')
```

### Step 16: Call permutation_cluster_1samp_test()

```python
permutation_cluster_1samp_test(condition1, threshold=1, stat_fun=lambda x: stat_fun(x)[:-1], out_type='mask')
```


## Complete Example

```python
# Setup
# Fixtures: numba_conditional, stat_fun

# Workflow
'Test cluster level permutations T-test.'
condition1_1d, _, condition1_2d, _ = _get_conditions()
for condition1, p in ((condition1_1d, 0.01), (condition1_2d, 0.01)):
    T_obs, clusters, cluster_p_values, hist = permutation_cluster_1samp_test(condition1, n_permutations=100, tail=0, seed=1, out_type='mask', buffer_size=None)
    assert_equal(np.sum(cluster_p_values < 0.05), 1)
    p_min = np.min(cluster_p_values)
    assert_allclose(p_min, p, atol=1e-06)
    T_obs_pos, _, cluster_p_values_pos, _ = permutation_cluster_1samp_test(condition1, n_permutations=100, tail=1, threshold=1.67, seed=1, stat_fun=stat_fun, out_type='mask', buffer_size=None)
    T_obs_neg, _, cluster_p_values_neg, _ = permutation_cluster_1samp_test(-condition1, n_permutations=100, tail=-1, threshold=-1.67, seed=1, stat_fun=stat_fun, buffer_size=None, out_type='mask')
    assert_array_equal(T_obs_pos, -T_obs_neg)
    assert_array_equal(cluster_p_values_pos < 0.05, cluster_p_values_neg < 0.05)
    buffer_size = condition1.shape[1] // 10
    with _record_warnings():
        T_obs_neg_buff, _, cluster_p_values_neg_buff, _ = permutation_cluster_1samp_test(-condition1, n_permutations=100, tail=-1, out_type='mask', threshold=-1.67, seed=1, n_jobs=2, stat_fun=stat_fun, buffer_size=buffer_size)
    assert_array_equal(T_obs_neg, T_obs_neg_buff)
    assert_array_equal(cluster_p_values_neg, cluster_p_values_neg_buff)
    with pytest.raises(TypeError, match='must be .* ndarray'):
        permutation_cluster_1samp_test(condition1, threshold=1, stat_fun=lambda x: None, out_type='mask')
    with pytest.raises(ValueError, match='not compatible'):
        permutation_cluster_1samp_test(condition1, threshold=1, stat_fun=lambda x: stat_fun(x)[:-1], out_type='mask')
```

## Next Steps


---

*Source: test_cluster_level.py:255 | Complexity: Advanced | Last updated: 2026-05-18*