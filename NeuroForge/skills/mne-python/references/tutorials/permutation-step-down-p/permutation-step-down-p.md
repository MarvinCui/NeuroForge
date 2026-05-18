# How To: Permutation Step Down P

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test cluster level permutations with step_down_p.

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

### Step 1: 'Test cluster level permutations with step_down_p.'

```python
'Test cluster level permutations with step_down_p.'
```

**Verification:**
```python
assert_equal(np.sum(p_old < 0.05), 1)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_allclose(p_min, 0.003906, atol=1e-06)
```

### Step 3: Assign X = rng.randn(...)

```python
X = rng.randn(9, 2, 10)
```

**Verification:**
```python
assert_equal(np.sum(p_new < 0.05), 2)
```

### Step 4: Assign thresh = 2

```python
thresh = 2
```

**Verification:**
```python
assert np.all(p_old >= p_new)
```

### Step 5: Assign unknown = permutation_cluster_1samp_test(...)

```python
t, clusters, p, H0 = permutation_cluster_1samp_test(X, threshold=thresh, step_down_p=1.0, out_type='mask')
```

**Verification:**
```python
assert_allclose(p_next, 0.015625, atol=1e-06)
```

### Step 6: Assign unknown = permutation_cluster_1samp_test(...)

```python
t, clusters, p_old, H0 = permutation_cluster_1samp_test(X, threshold=thresh, step_down_p=0.0, out_type='mask')
```

### Step 7: Call assert_equal()

```python
assert_equal(np.sum(p_old < 0.05), 1)
```

### Step 8: Assign p_min = np.min(...)

```python
p_min = np.min(p_old)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(p_min, 0.003906, atol=1e-06)
```

### Step 10: Assign unknown = permutation_cluster_1samp_test(...)

```python
t, clusters, p_new, H0 = permutation_cluster_1samp_test(X, threshold=thresh, step_down_p=0.05, out_type='mask')
```

### Step 11: Call assert_equal()

```python
assert_equal(np.sum(p_new < 0.05), 2)
```

**Verification:**
```python
assert np.all(p_old >= p_new)
```

### Step 12: Assign p_next = value

```python
p_next = p_new[(p_new > 0.004) & (p_new < 0.05)][0]
```

### Step 13: Call assert_allclose()

```python
assert_allclose(p_next, 0.015625, atol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: numba_conditional

# Workflow
'Test cluster level permutations with step_down_p.'
rng = np.random.RandomState(0)
X = rng.randn(9, 2, 10)
X[:, 0:2, 0:2] += 2
X[:, 1, 5:9] += 0.5
thresh = 2
t, clusters, p, H0 = permutation_cluster_1samp_test(X, threshold=thresh, step_down_p=1.0, out_type='mask')
t, clusters, p_old, H0 = permutation_cluster_1samp_test(X, threshold=thresh, step_down_p=0.0, out_type='mask')
assert_equal(np.sum(p_old < 0.05), 1)
p_min = np.min(p_old)
assert_allclose(p_min, 0.003906, atol=1e-06)
t, clusters, p_new, H0 = permutation_cluster_1samp_test(X, threshold=thresh, step_down_p=0.05, out_type='mask')
assert_equal(np.sum(p_new < 0.05), 2)
assert np.all(p_old >= p_new)
p_next = p_new[(p_new > 0.004) & (p_new < 0.05)][0]
assert_allclose(p_next, 0.015625, atol=1e-06)
```

## Next Steps


---

*Source: test_cluster_level.py:180 | Complexity: Advanced | Last updated: 2026-05-18*