# How To: Rank Epochs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that raw and epochs give the same results in a simple case.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne.cov`
- `mne.datasets`
- `mne.io`
- `mne.proj`
- `mne.rank`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: rank_method, proj
```

## Step-by-Step Guide

### Step 1: 'Test that raw and epochs give the same results in a simple case.'

```python
'Test that raw and epochs give the same results in a simple case.'
```

**Verification:**
```python
assert '{' not in log
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

**Verification:**
```python
assert rank_raw == rank_epochs
```

### Step 3: Assign epochs = make_fixed_length_epochs(...)

```python
epochs = make_fixed_length_epochs(raw, preload=True, proj=False)
```

### Step 4: Assign rank_raw = compute_rank(...)

```python
rank_raw = compute_rank(raw, rank_method, proj=proj)
```

### Step 5: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert '{' not in log
```

### Step 6: Assign rank_epochs = compute_rank(...)

```python
rank_epochs = compute_rank(epochs, rank_method, proj=proj)
```


## Complete Example

```python
# Setup
# Fixtures: rank_method, proj

# Workflow
'Test that raw and epochs give the same results in a simple case.'
raw = read_raw_fif(raw_fname, preload=True)
epochs = make_fixed_length_epochs(raw, preload=True, proj=False)
rank_raw = compute_rank(raw, rank_method, proj=proj)
with catch_logging(verbose=True) as log:
    rank_epochs = compute_rank(epochs, rank_method, proj=proj)
log = log.getvalue()
assert '{' not in log
assert rank_raw == rank_epochs
```

## Next Steps


---

*Source: test_rank.py:218 | Complexity: Intermediate | Last updated: 2026-05-18*