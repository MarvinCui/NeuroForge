# How To: Progressbar Parallel More

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ProgressBar with parallel computing, advanced version.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.parallel`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: capsys
```

## Step-by-Step Guide

### Step 1: 'Test ProgressBar with parallel computing, advanced version.'

```python
'Test ProgressBar with parallel computing, advanced version.'
```

**Verification:**
```python
assert capsys.readouterr().out == ''
```

### Step 2: Assign unknown = parallel_func(...)

```python
parallel, p_fun, _ = parallel_func(_identity_block_wide, n_jobs=1, verbose=False)
```

**Verification:**
```python
assert_array_equal(idxs, np.arange(len(arr) * 2))
```

### Step 3: Assign arr = np.arange(...)

```python
arr = np.arange(10)
```

**Verification:**
```python
assert Path(pb._mmap_fname).is_file()
```

### Step 4: Assign cap = capsys.readouterr(...)

```python
cap = capsys.readouterr()
```

**Verification:**
```python
assert sum_ == len(arr) * 2
```

### Step 5: Assign out = value

```python
out = cap.err
```

**Verification:**
```python
assert not Path(pb._mmap_fname).is_file(), '__exit__ not called?'
```

### Step 6: Assign out = parallel(...)

```python
out = parallel((p_fun(x, pb.subset(pb_idx)) for pb_idx, x in array_split_idx(arr, 2, n_per_split=2)))
```

**Verification:**
```python
assert '100%' in out
```

### Step 7: Assign idxs = np.concatenate(...)

```python
idxs = np.concatenate([o[1] for o in out])
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(idxs, np.arange(len(arr) * 2))
```

### Step 9: Assign out = np.concatenate(...)

```python
out = np.concatenate([o[0] for o in out])
```

**Verification:**
```python
assert Path(pb._mmap_fname).is_file()
```

### Step 10: Assign sum_ = np.memmap.sum(...)

```python
sum_ = np.memmap(pb._mmap_fname, dtype='bool', mode='r', shape=len(arr) * 2).sum()
```

**Verification:**
```python
assert sum_ == len(arr) * 2
```


## Complete Example

```python
# Setup
# Fixtures: capsys

# Workflow
'Test ProgressBar with parallel computing, advanced version.'
assert capsys.readouterr().out == ''
parallel, p_fun, _ = parallel_func(_identity_block_wide, n_jobs=1, verbose=False)
arr = np.arange(10)
with use_log_level(True):
    with ProgressBar(len(arr) * 2) as pb:
        out = parallel((p_fun(x, pb.subset(pb_idx)) for pb_idx, x in array_split_idx(arr, 2, n_per_split=2)))
        idxs = np.concatenate([o[1] for o in out])
        assert_array_equal(idxs, np.arange(len(arr) * 2))
        out = np.concatenate([o[0] for o in out])
        assert Path(pb._mmap_fname).is_file()
        sum_ = np.memmap(pb._mmap_fname, dtype='bool', mode='r', shape=len(arr) * 2).sum()
        assert sum_ == len(arr) * 2
assert not Path(pb._mmap_fname).is_file(), '__exit__ not called?'
cap = capsys.readouterr()
out = cap.err
assert '100%' in out
```

## Next Steps


---

*Source: test_progressbar.py:107 | Complexity: Advanced | Last updated: 2026-05-18*