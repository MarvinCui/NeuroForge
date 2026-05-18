# How To: Compute Proj Parallel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test computation of ExG projectors using parallelization.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.proj`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.ssp`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: short_raw
```

## Step-by-Step Guide

### Step 1: 'Test computation of ExG projectors using parallelization.'

```python
'Test computation of ExG projectors using parallelization.'
```

**Verification:**
```python
assert_array_almost_equal(projs, projs_2, 10)
```

### Step 2: Assign short_raw = short_raw.copy.pick.resample(...)

```python
short_raw = short_raw.copy().pick(('eeg', 'eog')).resample(100)
```

### Step 3: Assign raw = short_raw.copy(...)

```python
raw = short_raw.copy()
```

### Step 4: Assign raw_2 = short_raw.copy(...)

```python
raw_2 = short_raw.copy()
```

### Step 5: Assign projs = activate_proj(...)

```python
projs = activate_proj(projs)
```

### Step 6: Assign projs_2 = activate_proj(...)

```python
projs_2 = activate_proj(projs_2)
```

### Step 7: Assign unknown = make_projector(...)

```python
projs, _, _ = make_projector(projs, raw_2.info['ch_names'], bads=['MEG 2443'])
```

### Step 8: Assign unknown = make_projector(...)

```python
projs_2, _, _ = make_projector(projs_2, raw_2.info['ch_names'], bads=['MEG 2443'])
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(projs, projs_2, 10)
```

### Step 10: Assign unknown = compute_proj_eog(...)

```python
projs, _ = compute_proj_eog(raw, n_eeg=2, bads=raw.ch_names[1:2], average=False, avg_ref=True, no_proj=False, n_jobs=None, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=100)
```

### Step 11: Assign unknown = compute_proj_eog(...)

```python
projs_2, _ = compute_proj_eog(raw_2, n_eeg=2, bads=raw.ch_names[1:2], average=False, avg_ref=True, no_proj=False, n_jobs=2, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=100)
```


## Complete Example

```python
# Setup
# Fixtures: short_raw

# Workflow
'Test computation of ExG projectors using parallelization.'
short_raw = short_raw.copy().pick(('eeg', 'eog')).resample(100)
raw = short_raw.copy()
with pytest.warns(RuntimeWarning, match='Attenuation'):
    projs, _ = compute_proj_eog(raw, n_eeg=2, bads=raw.ch_names[1:2], average=False, avg_ref=True, no_proj=False, n_jobs=None, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=100)
raw_2 = short_raw.copy()
with _record_warnings(), pytest.warns(RuntimeWarning, match='Attenuation'):
    projs_2, _ = compute_proj_eog(raw_2, n_eeg=2, bads=raw.ch_names[1:2], average=False, avg_ref=True, no_proj=False, n_jobs=2, l_freq=None, h_freq=None, reject=None, tmax=dur_use, filter_length=100)
projs = activate_proj(projs)
projs_2 = activate_proj(projs_2)
projs, _, _ = make_projector(projs, raw_2.info['ch_names'], bads=['MEG 2443'])
projs_2, _, _ = make_projector(projs_2, raw_2.info['ch_names'], bads=['MEG 2443'])
assert_array_almost_equal(projs, projs_2, 10)
```

## Next Steps


---

*Source: test_ssp.py:164 | Complexity: Advanced | Last updated: 2026-05-18*