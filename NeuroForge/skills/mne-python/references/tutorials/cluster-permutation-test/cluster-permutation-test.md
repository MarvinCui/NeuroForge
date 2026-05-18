# How To: Cluster Permutation Test

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test cluster level permutations tests.

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
# Fixtures: numba_conditional
```

## Step-by-Step Guide

### Step 1: 'Test cluster level permutations tests.'

```python
'Test cluster level permutations tests.'
```

**Verification:**
```python
assert_equal(np.sum(cluster_p_values < 0.05), 1)
```

### Step 2: Assign unknown = _get_conditions(...)

```python
condition1_1d, condition2_1d, condition1_2d, condition2_2d = _get_conditions()
```

**Verification:**
```python
assert_allclose(p_min, 0.01, atol=1e-06)
```

### Step 3: Assign unknown = permutation_cluster_test(...)

```python
T_obs, clusters, cluster_p_values, hist = permutation_cluster_test([condition1, condition2], n_permutations=100, tail=1, seed=1, buffer_size=None, out_type='mask')
```

**Verification:**
```python
assert_array_equal(cluster_p_values, cluster_p_values_buff)
```

### Step 4: Assign p_min = np.min(...)

```python
p_min = np.min(cluster_p_values)
```

### Step 5: Call assert_equal()

```python
assert_equal(np.sum(cluster_p_values < 0.05), 1)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(p_min, 0.01, atol=1e-06)
```

### Step 7: Assign buffer_size = value

```python
buffer_size = condition1.shape[1] // 10
```

### Step 8: Assign unknown = permutation_cluster_test(...)

```python
T_obs, clusters, cluster_p_values_buff, hist = permutation_cluster_test([condition1, condition2], n_permutations=100, tail=1, seed=1, n_jobs=2, buffer_size=buffer_size, out_type='mask')
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(cluster_p_values, cluster_p_values_buff)
```

### Step 10: Call permutation_cluster_test()

```python
permutation_cluster_test([condition1, condition2], n_permutations=1, stat_fun=stat_fun, out_type='mask')
```


## Complete Example

```python
# Setup
# Fixtures: numba_conditional

# Workflow
'Test cluster level permutations tests.'
condition1_1d, condition2_1d, condition1_2d, condition2_2d = _get_conditions()
for condition1, condition2 in zip((condition1_1d, condition1_2d), (condition2_1d, condition2_2d)):
    T_obs, clusters, cluster_p_values, hist = permutation_cluster_test([condition1, condition2], n_permutations=100, tail=1, seed=1, buffer_size=None, out_type='mask')
    p_min = np.min(cluster_p_values)
    assert_equal(np.sum(cluster_p_values < 0.05), 1)
    assert_allclose(p_min, 0.01, atol=1e-06)
    buffer_size = condition1.shape[1] // 10
    T_obs, clusters, cluster_p_values_buff, hist = permutation_cluster_test([condition1, condition2], n_permutations=100, tail=1, seed=1, n_jobs=2, buffer_size=buffer_size, out_type='mask')
    assert_array_equal(cluster_p_values, cluster_p_values_buff)

def stat_fun(X, Y):
    return stats.f_oneway(X, Y)[0]
with pytest.warns(RuntimeWarning, match='is only valid'):
    permutation_cluster_test([condition1, condition2], n_permutations=1, stat_fun=stat_fun, out_type='mask')
```

## Next Steps


---

*Source: test_cluster_level.py:209 | Complexity: Advanced | Last updated: 2026-05-18*