# How To: Reg Rank

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test simple rank for cov regularization.

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

### Step 1: 'Test simple rank for cov regularization.'

```python
'Test simple rank for cov regularization.'
```

**Verification:**
```python
assert evoked.info['bads'] == []
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(ave_fname, condition=0, baseline=(None, 0), proj=False)
```

**Verification:**
```python
assert len(cov['names']) == 366
```

### Step 3: Assign cov = read_cov(...)

```python
cov = read_cov(cov_fname)
```

**Verification:**
```python
assert ranks == want_ranks
```

### Step 4: Assign unknown = value

```python
cov['bads'] = ['MEG 2443', 'EEG 053']
```

**Verification:**
```python
assert ranks == want_ranks
```

### Step 5: Assign want_ranks = dict(...)

```python
want_ranks = dict(meg=302, eeg=58)
```

### Step 6: Assign ranks = compute_rank(...)

```python
ranks = compute_rank(cov, info=evoked.info, rank=None)
```

**Verification:**
```python
assert ranks == want_ranks
```

### Step 7: Assign cov = regularize(...)

```python
cov = regularize(cov, evoked.info)
```

### Step 8: Assign ranks = compute_rank(...)

```python
ranks = compute_rank(cov, info=evoked.info, rank=None)
```

**Verification:**
```python
assert ranks == want_ranks
```


## Complete Example

```python
# Workflow
'Test simple rank for cov regularization.'
evoked = read_evokeds(ave_fname, condition=0, baseline=(None, 0), proj=False)
assert evoked.info['bads'] == []
cov = read_cov(cov_fname)
assert len(cov['names']) == 366
cov['bads'] = ['MEG 2443', 'EEG 053']
want_ranks = dict(meg=302, eeg=58)
ranks = compute_rank(cov, info=evoked.info, rank=None)
assert ranks == want_ranks
cov = regularize(cov, evoked.info)
ranks = compute_rank(cov, info=evoked.info, rank=None)
assert ranks == want_ranks
```

## Next Steps


---

*Source: test_cov.py:974 | Complexity: Advanced | Last updated: 2026-05-18*