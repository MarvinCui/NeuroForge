# How To: Compute Whitener Rank

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test risky rank options.

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `inspect`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.cov`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.rank`
- `mne.utils`
- `sklearn`


## Step-by-Step Guide

### Step 1: 'Test risky rank options.'

```python
'Test risky rank options.'
```

**Verification:**
```python
assert len(cov['names']) == 306
```

### Step 2: Assign info = read_info(...)

```python
info = read_info(ave_fname)
```

**Verification:**
```python
assert rank == 306
```

### Step 3: Assign info = pick_info(...)

```python
info = pick_info(info, pick_types(info, meg=True))
```

**Verification:**
```python
assert compute_rank(cov, info=info, verbose=True) == dict(meg=rank)
```

### Step 4: Assign cov = make_ad_hoc_cov._as_square(...)

```python
cov = make_ad_hoc_cov(info)._as_square()
```

**Verification:**
```python
assert rank == 305
```

### Step 5: Assign unknown = compute_whitener(...)

```python
_, _, rank = compute_whitener(cov, info, rank=None, return_rank=True)
```

**Verification:**
```python
assert compute_rank(cov, info=info, verbose=True) == dict(meg=rank)
```

### Step 6: Assign unknown = compute_whitener(...)

```python
_, _, rank = compute_whitener(cov, info, rank=None, return_rank=True)
```

**Verification:**
```python
assert rank == 306
```

### Step 7: Assign unknown = value

```python
info['projs'] = []
```

### Step 8: Assign unknown = compute_whitener(...)

```python
_, _, rank = compute_whitener(cov, info, rank=dict(meg=306), return_rank=True)
```


## Complete Example

```python
# Workflow
'Test risky rank options.'
info = read_info(ave_fname)
info = pick_info(info, pick_types(info, meg=True))
with info._unlock():
    info['projs'] = []
cov = make_ad_hoc_cov(info)._as_square()
assert len(cov['names']) == 306
_, _, rank = compute_whitener(cov, info, rank=None, return_rank=True)
assert rank == 306
assert compute_rank(cov, info=info, verbose=True) == dict(meg=rank)
cov['data'][-1] *= 1e-14
_, _, rank = compute_whitener(cov, info, rank=None, return_rank=True)
assert rank == 305
assert compute_rank(cov, info=info, verbose=True) == dict(meg=rank)
with pytest.warns(RuntimeWarning, match='orders of magnitude'), pytest.warns(RuntimeWarning, match='exceeds the estimated'):
    _, _, rank = compute_whitener(cov, info, rank=dict(meg=306), return_rank=True)
assert rank == 306
```

## Next Steps


---

*Source: test_cov.py:947 | Complexity: Advanced | Last updated: 2026-05-18*