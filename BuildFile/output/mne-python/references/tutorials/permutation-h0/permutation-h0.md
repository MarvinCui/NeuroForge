# How To: Permutation H0

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that H0 is populated properly during testing.

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

### Step 1: 'Test that H0 is populated properly during testing.'

```python
'Test that H0 is populated properly during testing.'
```

**Verification:**
```python
assert_equal(len(h0), 0)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_equal(len(h0), min(n_permutations, 64))
```

### Step 3: Assign data = value

```python
data = rng.rand(7, 10, 1) - 0.5
```

**Verification:**
```python
assert isinstance(clust[0], tuple)
```

### Step 4: Call assert_equal()

```python
assert_equal(len(h0), 0)
```

**Verification:**
```python
assert isinstance(clust[0], np.ndarray)
```

### Step 5: Assign unknown = spatio_temporal_cluster_1samp_test(...)

```python
t, clust, p, h0 = spatio_temporal_cluster_1samp_test(data, threshold=100, n_permutations=1024, seed=rng)
```

**Verification:**
```python
assert_equal(len(h0), 2 ** (7 - (tail == 0)))
```

### Step 6: Assign unknown = spatio_temporal_cluster_1samp_test(...)

```python
t, clust, p, h0 = spatio_temporal_cluster_1samp_test(data, threshold=0.1, n_permutations=n_permutations, seed=rng)
```

### Step 7: Call assert_equal()

```python
assert_equal(len(h0), min(n_permutations, 64))
```

**Verification:**
```python
assert isinstance(clust[0], tuple)
```

### Step 8: Assign unknown = spatio_temporal_cluster_1samp_test(...)

```python
t, clust, p, h0 = spatio_temporal_cluster_1samp_test(data, threshold=thresh, seed=rng, tail=tail, out_type='mask')
```

**Verification:**
```python
assert isinstance(clust[0], np.ndarray)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(h0), 2 ** (7 - (tail == 0)))
```


## Complete Example

```python
# Setup
# Fixtures: numba_conditional

# Workflow
'Test that H0 is populated properly during testing.'
rng = np.random.RandomState(0)
data = rng.rand(7, 10, 1) - 0.5
with pytest.warns(RuntimeWarning, match='No clusters found'):
    t, clust, p, h0 = spatio_temporal_cluster_1samp_test(data, threshold=100, n_permutations=1024, seed=rng)
assert_equal(len(h0), 0)
for n_permutations in (1024, 65, 64, 63):
    t, clust, p, h0 = spatio_temporal_cluster_1samp_test(data, threshold=0.1, n_permutations=n_permutations, seed=rng)
    assert_equal(len(h0), min(n_permutations, 64))
    assert isinstance(clust[0], tuple)
for tail, thresh in zip((-1, 0, 1), (-0.1, 0.1, 0.1)):
    t, clust, p, h0 = spatio_temporal_cluster_1samp_test(data, threshold=thresh, seed=rng, tail=tail, out_type='mask')
    assert isinstance(clust[0], np.ndarray)
    assert_equal(len(h0), 2 ** (7 - (tail == 0)))
```

## Next Steps


---

*Source: test_cluster_level.py:770 | Complexity: Advanced | Last updated: 2026-05-18*