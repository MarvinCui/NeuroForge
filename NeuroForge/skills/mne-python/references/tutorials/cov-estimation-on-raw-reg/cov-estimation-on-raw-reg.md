# How To: Cov Estimation On Raw Reg

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test estimation from raw with regularization.

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

### Step 1: 'Test estimation from raw with regularization.'

```python
'Test estimation from raw with regularization.'
```

**Verification:**
```python
assert_snr(cov.data, cov_mne.data, 5)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(raw._data[:, ::10].copy(), raw.info)
```

### Step 5: Assign cov_mne = read_cov(...)

```python
cov_mne = read_cov(erm_cov_fname)
```

### Step 6: Call assert_snr()

```python
assert_snr(cov.data, cov_mne.data, 5)
```

### Step 7: Assign cov = compute_raw_covariance(...)

```python
cov = compute_raw_covariance(raw, tstep=5.0, method='diagonal_fixed')
```


## Complete Example

```python
# Workflow
'Test estimation from raw with regularization.'
pytest.importorskip('sklearn')
raw = read_raw_fif(raw_fname, preload=True)
with raw.info._unlock():
    raw.info['sfreq'] /= 10.0
raw = RawArray(raw._data[:, ::10].copy(), raw.info)
cov_mne = read_cov(erm_cov_fname)
with _record_warnings(), pytest.warns(RuntimeWarning, match='Too few samples'):
    cov = compute_raw_covariance(raw, tstep=5.0, method='diagonal_fixed')
assert_snr(cov.data, cov_mne.data, 5)
```

## Next Steps


---

*Source: test_cov.py:399 | Complexity: Intermediate | Last updated: 2026-05-18*