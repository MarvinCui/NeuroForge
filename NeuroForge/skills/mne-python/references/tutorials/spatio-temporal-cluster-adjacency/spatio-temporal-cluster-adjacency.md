# How To: Spatio Temporal Cluster Adjacency

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test spatio-temporal cluster permutations.

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

### Step 1: 'Test spatio-temporal cluster permutations.'

```python
'Test spatio-temporal cluster permutations.'
```

**Verification:**
```python
assert_equal(np.sum(p_values_adj < 0.05), np.sum(p_values_no_adj < 0.05))
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert_array_equal(p_values_no_adj, p_values2)
```

### Step 3: Assign unknown = _get_conditions(...)

```python
condition1_1d, condition2_1d, condition1_2d, condition2_2d = _get_conditions()
```

### Step 4: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 5: Assign noise1_2d = rng.randn(...)

```python
noise1_2d = rng.randn(condition1_2d.shape[0], condition1_2d.shape[1], 10)
```

### Step 6: Assign data1_2d = np.transpose(...)

```python
data1_2d = np.transpose(np.dstack((condition1_2d, noise1_2d)), [0, 2, 1])
```

### Step 7: Assign noise2_d2 = rng.randn(...)

```python
noise2_d2 = rng.randn(condition2_2d.shape[0], condition2_2d.shape[1], 10)
```

### Step 8: Assign data2_2d = np.transpose(...)

```python
data2_2d = np.transpose(np.dstack((condition2_2d, noise2_d2)), [0, 2, 1])
```

### Step 9: Assign adj = grid_to_graph(...)

```python
adj = grid_to_graph(data1_2d.shape[-1], 1)
```

### Step 10: Assign threshold = dict(...)

```python
threshold = dict(start=4.0, step=2)
```

### Step 11: Assign unknown = spatio_temporal_cluster_test(...)

```python
T_obs, clusters, p_values_adj, hist = spatio_temporal_cluster_test([data1_2d, data2_2d], adjacency=adj, n_permutations=50, tail=1, seed=1, threshold=threshold, buffer_size=None)
```

### Step 12: Assign buffer_size = value

```python
buffer_size = data1_2d.size // 10
```

### Step 13: Assign unknown = spatio_temporal_cluster_test(...)

```python
T_obs, clusters, p_values_no_adj, hist = spatio_temporal_cluster_test([data1_2d, data2_2d], n_permutations=50, tail=1, seed=1, threshold=threshold, n_jobs=2, buffer_size=buffer_size)
```

### Step 14: Call assert_equal()

```python
assert_equal(np.sum(p_values_adj < 0.05), np.sum(p_values_no_adj < 0.05))
```

### Step 15: Assign unknown = spatio_temporal_cluster_test(...)

```python
T_obs, clusters, p_values2, _ = spatio_temporal_cluster_test([data1_2d, data2_2d], n_permutations=50, tail=1, seed=1, threshold=threshold, n_jobs=2, buffer_size=None)
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(p_values_no_adj, p_values2)
```

### Step 17: Call pytest.raises()

```python
pytest.raises(ValueError, spatio_temporal_cluster_test, [data1_2d, data2_2d], tail=1, threshold=-2.0)
```

### Step 18: Call pytest.raises()

```python
pytest.raises(ValueError, spatio_temporal_cluster_test, [data1_2d, data2_2d], tail=-1, threshold=2.0)
```

### Step 19: Call pytest.raises()

```python
pytest.raises(ValueError, spatio_temporal_cluster_test, [data1_2d, data2_2d], tail=0, threshold=-1)
```


## Complete Example

```python
# Setup
# Fixtures: numba_conditional

# Workflow
'Test spatio-temporal cluster permutations.'
pytest.importorskip('sklearn')
from sklearn.feature_extraction.image import grid_to_graph
condition1_1d, condition2_1d, condition1_2d, condition2_2d = _get_conditions()
rng = np.random.RandomState(0)
noise1_2d = rng.randn(condition1_2d.shape[0], condition1_2d.shape[1], 10)
data1_2d = np.transpose(np.dstack((condition1_2d, noise1_2d)), [0, 2, 1])
noise2_d2 = rng.randn(condition2_2d.shape[0], condition2_2d.shape[1], 10)
data2_2d = np.transpose(np.dstack((condition2_2d, noise2_d2)), [0, 2, 1])
adj = grid_to_graph(data1_2d.shape[-1], 1)
threshold = dict(start=4.0, step=2)
T_obs, clusters, p_values_adj, hist = spatio_temporal_cluster_test([data1_2d, data2_2d], adjacency=adj, n_permutations=50, tail=1, seed=1, threshold=threshold, buffer_size=None)
buffer_size = data1_2d.size // 10
T_obs, clusters, p_values_no_adj, hist = spatio_temporal_cluster_test([data1_2d, data2_2d], n_permutations=50, tail=1, seed=1, threshold=threshold, n_jobs=2, buffer_size=buffer_size)
assert_equal(np.sum(p_values_adj < 0.05), np.sum(p_values_no_adj < 0.05))
T_obs, clusters, p_values2, _ = spatio_temporal_cluster_test([data1_2d, data2_2d], n_permutations=50, tail=1, seed=1, threshold=threshold, n_jobs=2, buffer_size=None)
assert_array_equal(p_values_no_adj, p_values2)
pytest.raises(ValueError, spatio_temporal_cluster_test, [data1_2d, data2_2d], tail=1, threshold=-2.0)
pytest.raises(ValueError, spatio_temporal_cluster_test, [data1_2d, data2_2d], tail=-1, threshold=2.0)
pytest.raises(ValueError, spatio_temporal_cluster_test, [data1_2d, data2_2d], tail=0, threshold=-1)
```

## Next Steps


---

*Source: test_cluster_level.py:649 | Complexity: Advanced | Last updated: 2026-05-18*