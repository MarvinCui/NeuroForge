# How To: Permutation Cluster Signs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test cluster signs.

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
# Fixtures: threshold, kind
```

## Step-by-Step Guide

### Step 1: 'Test cluster signs.'

```python
'Test cluster signs.'
```

**Verification:**
```python
assert kind == 'ind'
```

### Step 2: Assign X = np.array(...)

```python
X = np.array([[[-10, 5], [-2, -7]], [[-4, 5], [-8, -0]], [[-6, 3], [-4, -2]]], float)
```

**Verification:**
```python
assert len(clu) == len(clu_pvalues)
```

### Step 3: Assign want_signs = np.sign(...)

```python
want_signs = np.sign(np.mean(X, axis=0))
```

**Verification:**
```python
assert not used[c].any()
```

### Step 4: Assign n_permutations = 1

```python
n_permutations = 1
```

**Verification:**
```python
assert len(np.unique(np.sign(tobs[c]))) == 1
```

### Step 5: Assign unknown = func(...)

```python
tobs, clu, clu_pvalues, _ = func(use_X, n_permutations=n_permutations, threshold=threshold, tail=0, stat_fun=stat_fun, out_type='mask')
```

**Verification:**
```python
assert used.all()
```

### Step 6: Assign clu_signs = np.zeros(...)

```python
clu_signs = np.zeros(X.shape[1:])
```

**Verification:**
```python
assert clu_signs.all()
```

### Step 7: Assign used = np.zeros(...)

```python
used = np.zeros(X.shape[1:])
```

**Verification:**
```python
assert_array_equal(np.sign(tobs), want_signs)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(np.sign(tobs), want_signs)
```

**Verification:**
```python
assert_array_equal(clu_signs, want_signs)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(clu_signs, want_signs)
```

### Step 10: Assign func = permutation_cluster_1samp_test

```python
func = permutation_cluster_1samp_test
```

### Step 11: Assign stat_fun = ttest_1samp_no_p

```python
stat_fun = ttest_1samp_no_p
```

### Step 12: Assign use_X = X

```python
use_X = X
```

**Verification:**
```python
assert kind == 'ind'
```

### Step 13: Assign func = permutation_cluster_test

```python
func = permutation_cluster_test
```

### Step 14: Assign stat_fun = ttest_ind_no_p

```python
stat_fun = ttest_ind_no_p
```

### Step 15: Assign use_X = value

```python
use_X = [X, np.random.RandomState(0).randn(*X.shape) * 0.1]
```

**Verification:**
```python
assert not used[c].any()
```

### Step 16: Assign unknown = value

```python
clu_signs[c] = np.sign(tobs[c])[0]
```

### Step 17: Assign unknown = True

```python
used[c] = True
```


## Complete Example

```python
# Setup
# Fixtures: threshold, kind

# Workflow
'Test cluster signs.'
X = np.array([[[-10, 5], [-2, -7]], [[-4, 5], [-8, -0]], [[-6, 3], [-4, -2]]], float)
want_signs = np.sign(np.mean(X, axis=0))
n_permutations = 1
if kind == '1samp':
    func = permutation_cluster_1samp_test
    stat_fun = ttest_1samp_no_p
    use_X = X
else:
    assert kind == 'ind'
    func = permutation_cluster_test
    stat_fun = ttest_ind_no_p
    use_X = [X, np.random.RandomState(0).randn(*X.shape) * 0.1]
tobs, clu, clu_pvalues, _ = func(use_X, n_permutations=n_permutations, threshold=threshold, tail=0, stat_fun=stat_fun, out_type='mask')
clu_signs = np.zeros(X.shape[1:])
used = np.zeros(X.shape[1:])
assert len(clu) == len(clu_pvalues)
for c, p in zip(clu, clu_pvalues):
    assert not used[c].any()
    assert len(np.unique(np.sign(tobs[c]))) == 1
    clu_signs[c] = np.sign(tobs[c])[0]
    used[c] = True
assert used.all()
assert clu_signs.all()
assert_array_equal(np.sign(tobs), want_signs)
assert_array_equal(clu_signs, want_signs)
```

## Next Steps


---

*Source: test_cluster_level.py:531 | Complexity: Advanced | Last updated: 2026-05-18*