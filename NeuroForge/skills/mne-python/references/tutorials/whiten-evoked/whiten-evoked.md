# How To: Whiten Evoked

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test whitening of evoked data.

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

### Step 1: 'Test whitening of evoked data.'

```python
'Test whitening of evoked data.'
```

**Verification:**
```python
assert np.all(mean_baseline < 1.0)
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(ave_fname, condition=0, baseline=(None, 0), proj=True)
```

**Verification:**
```python
assert np.all(mean_baseline > 0.2)
```

### Step 3: Assign cov = read_cov(...)

```python
cov = read_cov(cov_fname)
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(evoked.info, meg=True, eeg=True, ref_meg=False, exclude='bads')
```

### Step 5: Assign noise_cov = regularize(...)

```python
noise_cov = regularize(cov, evoked.info, grad=0.1, mag=0.1, eeg=0.1, exclude='bads', rank='full')
```

### Step 6: Assign evoked_white = whiten_evoked(...)

```python
evoked_white = whiten_evoked(evoked, noise_cov, picks, diag=True)
```

### Step 7: Assign whiten_baseline_data = value

```python
whiten_baseline_data = evoked_white.data[picks][:, evoked.times < 0]
```

### Step 8: Assign mean_baseline = np.mean(...)

```python
mean_baseline = np.mean(np.abs(whiten_baseline_data), axis=1)
```

**Verification:**
```python
assert np.all(mean_baseline < 1.0)
```

### Step 9: Assign cov_bad = pick_channels_cov(...)

```python
cov_bad = pick_channels_cov(cov, include=evoked.ch_names[:10])
```

### Step 10: Call pytest.raises()

```python
pytest.raises(RuntimeError, whiten_evoked, evoked, cov_bad, picks)
```


## Complete Example

```python
# Workflow
'Test whitening of evoked data.'
evoked = read_evokeds(ave_fname, condition=0, baseline=(None, 0), proj=True)
cov = read_cov(cov_fname)
picks = pick_types(evoked.info, meg=True, eeg=True, ref_meg=False, exclude='bads')
noise_cov = regularize(cov, evoked.info, grad=0.1, mag=0.1, eeg=0.1, exclude='bads', rank='full')
evoked_white = whiten_evoked(evoked, noise_cov, picks, diag=True)
whiten_baseline_data = evoked_white.data[picks][:, evoked.times < 0]
mean_baseline = np.mean(np.abs(whiten_baseline_data), axis=1)
assert np.all(mean_baseline < 1.0)
assert np.all(mean_baseline > 0.2)
cov_bad = pick_channels_cov(cov, include=evoked.ch_names[:10])
pytest.raises(RuntimeError, whiten_evoked, evoked, cov_bad, picks)
```

## Next Steps


---

*Source: test_cov.py:578 | Complexity: Advanced | Last updated: 2026-05-18*