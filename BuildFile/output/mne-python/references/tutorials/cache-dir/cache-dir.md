# How To: Cache Dir

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test use of cache dir.

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
# Fixtures: tmp_path, numba_conditional
```

## Step-by-Step Guide

### Step 1: 'Test use of cache dir.'

```python
'Test use of cache dir.'
```

**Verification:**
```python
assert 'independently' not in log_file.getvalue()
```

### Step 2: Assign tempdir = str(...)

```python
tempdir = str(tmp_path)
```

### Step 3: Assign orig_dir = os.getenv(...)

```python
orig_dir = os.getenv('MNE_CACHE_DIR', None)
```

### Step 4: Assign orig_size = os.getenv(...)

```python
orig_size = os.getenv('MNE_MEMMAP_MIN_SIZE', None)
```

### Step 5: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 6: Assign X = rng.randn(...)

```python
X = rng.randn(9, 2, 10)
```

### Step 7: Assign unknown = '1K'

```python
os.environ['MNE_MEMMAP_MIN_SIZE'] = '1K'
```

### Step 8: Assign unknown = tempdir

```python
os.environ['MNE_CACHE_DIR'] = tempdir
```

**Verification:**
```python
assert 'independently' not in log_file.getvalue()
```

### Step 9: Assign stat_fun = partial(...)

```python
stat_fun = partial(ttest_1samp_no_p, sigma=0.001)
```

### Step 10: Assign random_state = np.random.default_rng(...)

```python
random_state = np.random.default_rng(0)
```

### Step 11: Call permutation_cluster_1samp_test()

```python
permutation_cluster_1samp_test(X, buffer_size=None, n_jobs=2, n_permutations=1, seed=0, stat_fun=ttest_1samp_no_p, verbose=False, out_type='mask')
```

### Step 12: Call permutation_cluster_1samp_test()

```python
permutation_cluster_1samp_test(X, buffer_size=10, n_jobs=2, n_permutations=1, seed=random_state, stat_fun=stat_fun, verbose=False, out_type='mask')
```

### Step 13: Assign unknown = orig_dir

```python
os.environ['MNE_CACHE_DIR'] = orig_dir
```

### Step 14: Assign unknown = orig_size

```python
os.environ['MNE_MEMMAP_MIN_SIZE'] = orig_size
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, numba_conditional

# Workflow
'Test use of cache dir.'
tempdir = str(tmp_path)
orig_dir = os.getenv('MNE_CACHE_DIR', None)
orig_size = os.getenv('MNE_MEMMAP_MIN_SIZE', None)
rng = np.random.RandomState(0)
X = rng.randn(9, 2, 10)
try:
    os.environ['MNE_MEMMAP_MIN_SIZE'] = '1K'
    os.environ['MNE_CACHE_DIR'] = tempdir
    with catch_logging() as log_file:
        permutation_cluster_1samp_test(X, buffer_size=None, n_jobs=2, n_permutations=1, seed=0, stat_fun=ttest_1samp_no_p, verbose=False, out_type='mask')
    assert 'independently' not in log_file.getvalue()
    stat_fun = partial(ttest_1samp_no_p, sigma=0.001)
    random_state = np.random.default_rng(0)
    with _record_warnings(), pytest.warns(RuntimeWarning, match='independently'):
        permutation_cluster_1samp_test(X, buffer_size=10, n_jobs=2, n_permutations=1, seed=random_state, stat_fun=stat_fun, verbose=False, out_type='mask')
finally:
    if orig_dir is not None:
        os.environ['MNE_CACHE_DIR'] = orig_dir
    else:
        del os.environ['MNE_CACHE_DIR']
    if orig_size is not None:
        os.environ['MNE_MEMMAP_MIN_SIZE'] = orig_size
    else:
        del os.environ['MNE_MEMMAP_MIN_SIZE']
```

## Next Steps


---

*Source: test_cluster_level.py:119 | Complexity: Advanced | Last updated: 2026-05-18*